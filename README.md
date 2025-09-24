# Home Assistant Blueprints by Tipana

## IR Keypad → Zigbee2MQTT (Generic labels, optional energy monitoring)

One blueprint to control **any IR device** via a dropdown (`input_select`) and a Zigbee2MQTT IR blaster.

**Import:**  
Paste this raw URL in Home Assistant → Settings → Automations & Scenes → Blueprints → Import:
https://raw.githubusercontent.com/Tipana/home-assistant-blueprints/main/blueprints/automation/tipana/ir_keypad_z2m_generic.yaml

**Setup (per device):**
1. Create an `input_select` with your button labels (e.g. `On`, `Off`, `Speed Up`, …).
2. (Optional) Create `input_boolean.ir_resetting` to guard “snap-back” loops.
3. (Optional) Provide a smart-plug power sensor + ON watts threshold, or a helper boolean for power state.
4. Create an automation from the blueprint and:
   - Set your **Zigbee2MQTT topic** (e.g. `zigbee2mqtt/IR_Blaster_Parents_Bedroom/set`)
   - Enter **power labels** exactly as they appear (defaults to `On`/`Off`)
   - Choose **toggle** power code *or* distinct **ON/OFF** codes
   - Paste a JSON map of other labels → base64 IR codes (example below)

**Example `actions_map_json`:**
```json
{
  "Speed Up": "ByAjTxFwAgY...==",
  "Speed Down": "BxojRxFpAgA...==",
  "Swing Up": "Bw8jVBFfAhk...==",
  "Swing Down": "Bx4jahFrAgY...==",
  "Left": "BxAjUxFpAgg...==",
  "Right": "BR4jURE6AuA...==",
  "Burst": "BiUjRhFrAgh...==",
  "Sensor": "Cd8jkRFcAvw...==",
  "Timer": "B9QjdBF2Av4...=="
}
---

Notes:
	•	Uses energy sensor if provided (best), else a helper boolean.
	•	Prevents wrong-way power toggles using state inference.
	•	Snaps your dropdown back to the “On” label after non-power actions.