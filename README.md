# Home Assistant Blueprints by Tipana

## IR Keypad → Zigbee2MQTT (Generic, with examples inside Blueprint)

This blueprint lets you control **any IR device** (fan, heater, TV, AC, etc.) via an `input_select` and a Zigbee2MQTT IR blaster — using your own labels.

---

## 📑 Table of Contents
- [📥 Import](#-import)
- [ℹ️ Instructions](#ℹ️-instructions)
- [🖼 Example Input Select](#-example-input-select)
- [🖥 Optional Debug Cards](#-optional-debug-cards)
  - [Fan Debug Card](#fan-debug-card)
  - [Heater Debug Card](#heater-debug-card)
- [🛠 Maintainer & License](#-maintainer--license)

---

### 📥 Import
Paste this URL in Home Assistant → Settings → Automations & Scenes → Blueprints → Import:

```
https://raw.githubusercontent.com/Tipana/home-assistant-blueprints/main/blueprints/automation/tipana/ir_keypad_z2m_generic.yaml
```

---

### ℹ️ Instructions
- Full setup notes, examples, and JSON maps are included **directly inside the blueprint description** in Home Assistant.
- Once imported, create **one automation per device** (fan, heater, TV, etc.) with its own labels and IR codes.

---

### 🖼 Example Input Select
Here’s what a simple `input_select` dropdown looks like in Lovelace:

![Example Input Select](https://raw.githubusercontent.com/Tipana/home-assistant-blueprints/main/images/input_select_example.png)


---

## 🖥 Optional Debug Cards

Copy/paste these YAML snippets into a **Lovelace dashboard** to help debug your IR setup:

- **Entities card** shows the dropdown, helper booleans, guard, and energy sensors.  
- **Logbook card** shows recent state changes (so you can confirm when IR codes are firing and when snap-back happens).  
- Adjust the entity IDs (`input_select.fan_control`, `sensor.heater_power_watts`, etc.) to match your setup.  

---

### Fan Debug Card

```yaml
type: vertical-stack
cards:
  - type: entities
    title: IR Debug - Fan
    entities:
      - entity: input_select.fan_control
        name: Fan Control (remote)
      - entity: input_boolean.shark_fan_parents_is_on
        name: Fan Power Helper
      - entity: sensor.fan_power_watts
        name: Fan Power (W)
      - entity: input_boolean.ir_resetting
        name: IR Reset Guard

  - type: logbook
    title: Last Fan Events
    entities:
      - input_select.fan_control
      - input_boolean.shark_fan_parents_is_on
      - sensor.fan_power_watts
    hours_to_show: 4
```

📸 Screenshot placeholder:  
![Fan Debug Card](https://raw.githubusercontent.com/Tipana/home-assistant-blueprints/main/images/fan_debug_card.png)

---

### Heater Debug Card

```yaml
type: vertical-stack
cards:
  - type: entities
    title: IR Debug - Heater
    entities:
      - entity: input_select.heater_control
        name: Heater Control (remote)
      - entity: input_boolean.heater_parents_is_on
        name: Heater Power Helper
      - entity: sensor.heater_power_watts
        name: Heater Power (W)
      - entity: input_boolean.ir_resetting
        name: IR Reset Guard

  - type: logbook
    title: Last Heater Events
    entities:
      - input_select.heater_control
      - input_boolean.heater_parents_is_on
      - sensor.heater_power_watts
    hours_to_show: 4
```

📸 Screenshot placeholder:  
![Heater Debug Card](https://raw.githubusercontent.com/Tipana/home-assistant-blueprints/main/images/heater_debug_card.png)

---

## 🛠 Maintainer & License
Maintained by [Tipana](https://github.com/Tipana)  
License: MIT
