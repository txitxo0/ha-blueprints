# My Home Assistant Blueprints

Home Assistant blueprints for energy optimization.

## ⚡ Appliance Lifecycle Manager (v0.2)

The Appliance Orchestrator Pro is an agnostic lifecycle manager designed to handle any appliance (Dishwasher, Washing Machine, Dryer) by monitoring power consumption and energy schedules.

### 🌟 Features
- **Smart Admission Control:** Automatically pauses the appliance if started outside the cheap energy window or if there isn't enough time to finish the cycle.
- **Customizable Notifications:** You can define your own messages for waiting, error, and completion states. Supports Jinja2 templates for timestamps.
- **Watchdog Protection:** Detects if an appliance was turned on but failed to start (e.g., door left open) and sends a high-priority alert.
- **Intelligent Bypass:** Interactive mobile notifications allow you to "Start Now" and override the energy schedule for 5 minutes.
- **Auto-Cleanup:** Clean notification management using unique tags to prevent clutter.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ftxitxo0%2Fha-blueprints%2Fblob%2Fmain%2Fblueprints%2Fautomation%2Fenergy%2Fappliance_lifecycle_manager.yaml)

---

## 🛠 Prerequisites
1. **Status Helper:** Create an input_select with the following exact options:
    - `IDLE`, `RUNNING`, `WAITING_FOR_WINDOW`, `ERROR`.
1. **Energy Schedule:** A schedule entity defining your "Cheap/Valle" hours.
1. **Power Monitoring:** A smart plug or sensor with power (W) reporting.
1. **Notification Service:** Use a valid mobile notification service.

## 📂 Repository Structure
This repository is organized by domain to allow for future expansion:
- `/energy`: Power management and appliance orchestration.
- `/script`: (Comming soon) Transformers from different ligth tiers to an HA schedule
## ⚖️ License
Licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).