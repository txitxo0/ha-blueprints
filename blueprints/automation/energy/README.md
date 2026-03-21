# ⚡ Appliance Orchestrator Pro

Smart lifecycle manager for home appliances with energy schedule awareness, watchdog protection and actionable notifications. Designed to be fully agnostic — works with any appliance that has power monitoring (dishwasher, washing machine, dryer, etc.).

---

## Features

- **Smart admission control** — automatically delays the appliance if started outside the cheap energy window or if there is not enough time left to complete the cycle
- **Intelligent bypass** — interactive mobile notification lets you override the energy schedule and start immediately
- **Watchdog protection** — detects if an appliance was turned on but failed to draw power (e.g. door left open) and sends a high-priority alert
- **Anomaly detection** — flags cycles that finish abnormally short or long compared to the expected duration
- **Customizable notifications** — define your own messages for waiting, error and completion states with Jinja2 template support
- **Auto-cleanup** — notification tags are auto-generated from the automation entity ID, preventing clutter and supporting multiple instances

---

## Requirements

- A smart plug or power sensor reporting consumption in watts (`sensor.*`, device class `power`)
- A switch entity to control the appliance (`switch.*`)
- An `input_select` helper with the following **exact** options: `IDLE`, `RUNNING`, `WAITING_FOR_WINDOW`, `ERROR`
- A schedule entity defining your cheap/off-peak energy hours
- Home Assistant Companion App installed on the target device

---

## Inputs

| Input | Description |
|---|---|
| **Appliance Name** | Display name used in notification titles |
| **Smart Plug** | Switch entity controlling the appliance |
| **Power Sensor** | Sensor reporting live power draw (W) |
| **Status Input Select** | `input_select` helper tracking the appliance lifecycle state |
| **Energy Schedule** | Schedule entity defining cheap energy windows |
| **Start-up Power (W)** | Power threshold above which the cycle is considered started (default: 3 W) |
| **Working Power Threshold (W)** | Minimum power to confirm the appliance is actively running (default: 15 W) |
| **End-of-cycle Power (W)** | Power threshold below which the cycle is considered finished (default: 2 W) |
| **Expected Cycle Duration (min)** | Reference duration used for watchdog and anomaly detection (default: 70 min) |
| **Watchdog/End Delay (min)** | How long power must stay below end threshold before triggering end-of-cycle (default: 3 min) |
| **Notification Service** | Target notify service, e.g. `notify.mobile_app_pixel_8` or `notify.family` (see note below) |
| **Message: Paused** | Notification body when delayed due to energy schedule |
| **Label: Bypass Button** | Label for the bypass action button in the paused notification |
| **Message: Error** | Notification body on startup failure or door-open detection |
| **Message: Anomaly** | Notification body when cycle ends outside expected duration range |
| **Message: Finished** | Notification body on successful cycle completion (supports Jinja2, e.g. `{{ now().strftime('%H:%M') }}`) |
| **Action: On Pause** | Optional action sequence triggered on pause |
| **Action: On Error/Anomaly** | Optional action sequence triggered on error or anomaly |
| **Action: On Finished** | Optional action sequence triggered on successful completion |

---

## Notification Service

Any valid `notify.*` service works, including notification groups. Groups are not configurable through the UI and must be defined in `configuration.yaml`:

```yaml
notify:
  - name: family
    platform: group
    services:
      - service: mobile_app_pixel_8_jesus
      - service: mobile_app_partner_phone
```

After adding this, restart Home Assistant. The group will be available as `notify.family`.

---

## Status Helper Setup

Before instantiating this blueprint, create an `input_select` helper with the following exact options:

```
IDLE
RUNNING
WAITING_FOR_WINDOW
ERROR
```

Go to **Settings → Devices & Services → Helpers → Create Helper → Dropdown** and add the four options above.

---

## Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/txitxo0/ha-blueprints/main/blueprints/automation/energy/appliance_lifecycle_manager.yaml)

Or import manually:

1. Go to **Settings → Automations & Scenes → Blueprints**
2. Click **Import Blueprint**
3. Paste the URL of this file

---

## Lifecycle State Machine

```
IDLE ──► RUNNING ──► IDLE (success)
  │          │
  │          └──► ERROR (startup failure / anomaly)
  │
  └──► WAITING_FOR_WINDOW ──► RUNNING (window opens or bypass)
```

---

## Notes

- The watchdog uses the expected cycle duration as a reference: cycles finishing in less than 5% of the reference are flagged as startup errors, cycles between 75% and 150% are considered successful
- Multiple instances of this blueprint for different appliances will not interfere with each other as each notification tag is derived from the automation's own entity ID
- The bypass button is only shown while the appliance is in `WAITING_FOR_WINDOW` state
