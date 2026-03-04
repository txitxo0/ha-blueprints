# Home Assistant Blueprints

A growing collection of blueprints for energy-aware home automation.

---

## Blueprints
### ⚡ Appliance Orchestrator Pro — `v1.3.1-beta` ·

[![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ftxitxo0%2Fha-blueprints%2Fblob%2Fbeta%2Fblueprints%2Fautomation%2Fenergy%2Fappliance_lifecycle_manager.yaml)

Agnostic lifecycle manager for any power-monitored appliance (washing machine, dishwasher, dryer). Orchestrates the full cycle against an energy schedule: holds the appliance in a waiting state outside cheap hours, resumes automatically when the window opens, and validates the cycle duration to detect failures.

**State machine:** `IDLE` → `WAITING_FOR_WINDOW` ↔ `RUNNING` → `IDLE` / `ERROR`

**Key behaviors:**
- Admission control: blocks start if outside the cheap window or if remaining time is insufficient to complete the cycle
- Watchdog: detects start failures (e.g. door left open) and anomalous cycle durations
- Actionable notifications: "Start Now" bypass delivered to mobile, auto-cleared after 5 minutes
- All notification messages are user-defined and support Jinja2 templates
- Custom actions on pause, error, and completion

#### 🛠 Prerequisites 

1. `input_select` helper with options: `IDLE`, `RUNNING`, `WAITING_FOR_WINDOW`, `ERROR`
2. HA `schedule` entity defining cheap energy hours
3. Smart plug or sensor reporting power in W
4. Mobile notification service (e.g. `notify.mobile_app_iphone`)

> [!TIP]
> To notify multiple people, use a notification group in `configuration.yaml`:
> ```yaml
> notify:
>   - name: family
>     platform: group
>     services:
>       - service: mobile_app_person1
>       - service: mobile_app_person2
> ```

---

## 🌟 Roadmap

- **PVPC → Schedule parser** — automation blueprint that reads the Spanish PVPC electricity price feed and materializes cheap hours into a native HA `schedule` entity, making it a drop-in input for the Orchestrator
- Additional price feed parsers (Octopus Energy, generic ENTSO-E)
- Multi-appliance coordination (queue management)

---

## 📂 Repository Structure
```
blueprints/
└── automation/
    └── energy/
        ├── appliance_lifecycle_manager.yaml
        └── (upcoming parsers)
```

---

## ⚖️ License

[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)