# Spa Electrics GKRX Multi Plus Pool Light Control for Home Assistant

This repository contains the YAML configuration I use in Home Assistant to control the colour of my Spa Electrics GKRX Multi Plus pool light.

The light is controlled by briefly switching power off and back on, which advances the pool light to the next colour/program mode. Home Assistant keeps track of the selected colour so it can be shown on the dashboard.

![Pool Light Dashboard](dashboard.png)

## What this does

This setup allows Home Assistant to:

- Turn the pool light on and off
- Step the light to the next colour
- Track the currently selected colour
- Display the current colour on a dashboard
- Automatically turn the pool light off after a set time
- Provide script-based control so the logic can be reused from buttons, automations, or dashboards

## Files included

### `configuration.yaml`

Contains the required Home Assistant helper entities and relevant configuration.

This may include things such as:

- Current colour tracking
- Colour selection helpers
- Input buttons or template entities used by the dashboard and automations

Only the relevant parts of my full `configuration.yaml` are included.

### `scripts.yaml`

Contains the scripts that perform the actual pool light control actions.

The main logic is:

1. Turn the pool light relay off briefly
2. Turn it back on
3. Advance the stored colour value in Home Assistant
4. Keep the dashboard in sync with the real pool light colour

This is needed because the Spa Electrics light does not expose a smart colour-control API. It changes colour by cycling power.

### `automations.yaml`

Contains the automations used for the pool light.

These include:

- Handling the “Next Colour” button
- Updating the current colour helper
- Automatically turning the light off after the configured time

Only the relevant pool light automation code is included.

## How the colour control works

Spa Electrics multi-colour pool lights normally change colour when the power is toggled off and back on.

Home Assistant cannot directly tell the light to “go blue” or “go green”. Instead, this setup keeps track of the current colour and advances through the colour list each time the light is cycled.

Example:

```text
White → Blue → Green → Red → Purple → Aqua → Next Mode
