# My Home Assistant Blueprints

Home Assistant blueprints for energy optimization.

## ⚡ Appliance Lifecycle Manager (v0.1)

### 🌟 Features
- **Admission Control:** Automatically pauses appliances during expensive hours.
- **Customizable Notifications:** You can define your own messages for waiting, error, and completion states. Supports Jinja2 templates for timestamps.
- **Dynamic Tagging:** Unique session IDs (`entity_id` + `timestamp`) for perfect notification cleanup.
- **Auto-Cleanup:** Notifications are cleared after a timeout or when the cycle resumes.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ftxitxo0%2Fha-blueprints%2Fblob%2Fmain%2Fblueprints%2Fautomation%2Fenergy%2Fappliance_lifecycle_manager.yaml)

---

## 🛠 Prerequisites
1. **Input Select:** Create a helper with options `IDLE`, `WASHING`, `WAITING_FOR_WINDOW`, `ERROR`.
2. **Notification Service:** Use a valid mobile notification service.

## ⚖️ License
Licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).