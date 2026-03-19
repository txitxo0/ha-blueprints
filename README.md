# 📦 ha-blueprints

A collection of Home Assistant blueprints organized by domain. Each blueprint lives in its own folder with dedicated documentation.

> Licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)

---

## ⚡ Energy

### [Appliance Orchestrator Pro](./blueprints/automation/energy/appliance_lifecycle_manager.yaml)

Smart lifecycle manager for home appliances with energy schedule awareness, watchdog protection and actionable notifications. Delays appliance start until off-peak energy windows, monitors the cycle and notifies on completion, anomaly or error.

→ [Documentation](./blueprints/automation/energy/README.md)

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/txitxo0/ha-blueprints/main/blueprints/automation/energy/appliance_lifecycle_manager.yaml)

---

## 🧹 Cleaning

### [Vacuum Notification Card](./blueprints/automation/cleaning/vacuum_notification_card.yaml)

Persistent Android notification card for robot vacuums. Shows live status, tank level and a live map snapshot while cleaning. Sends a completion notification with the final map on dock. Fully controllable from the notification.

→ [Documentation](./blueprints/automation/cleaning/README.md)

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/txitxo0/ha-blueprints/main/blueprints/automation/cleaning/vacuum_notification_card.yaml)

---

## Repository Structure

```
blueprints/
└── automation/
    ├── energy/
    │   ├── appliance_lifecycle_manager.yaml
    │   └── README.md
    └── cleaning/
        ├── vacuum_notification_card.yaml
        └── README.md
```

---

## Contributing

Feel free to open an issue or PR if you find a bug or want to suggest an improvement.
