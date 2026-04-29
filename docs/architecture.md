# Firmware Architecture (Documentation-first, behavior-preserving)

## Goal

Organize the project so existing firmware logic is preserved while documentation and maintainability improve.

## Recommended MicroPython layout

- `src/main.py`
  - Existing application entrypoint and control loop (unchanged logic).
- `lib/`
  - Optional reusable modules if you later split code without changing behavior:
    - `keypad.py` (matrix scan)
    - `led_panel.py` (12-output mapping)
    - `config.py` (pins, timings)
- `docs/`
  - Hardware and architecture reference.

## Runtime flow (typical)

1. Initialize GPIO directions and pull configurations.
2. Initialize LED outputs to known safe state (usually OFF).
3. Repeatedly scan keypad matrix.
4. Translate key events to LED state changes according to existing logic.
5. Optionally print diagnostics over UART (`GP0/GP1`).

## Pin-domain separation

- **Input domain**: keypad columns/rows (`GP16..GP22`, `GP26`)
- **Output domain**: LEDs (`GP2..GP11`, `GP27`, `GP28`)
- **Support domain**: serial + power rails

This separation helps avoid accidental direction conflicts when maintaining firmware.

## Behavior preservation policy

For this repository cleanup:
- Keep the original `main.py` logic unchanged.
- Only relocate files and improve documentation.
- If naming is normalized (e.g., `main.py`), preserve exact runtime semantics.

## Wokwi vs hardware parity checklist

- Match GPIO assignments exactly.
- Keep LED resistor values at 220Ω.
- Keep keypad row pull-ups present (external or equivalent).
- Validate key debounce and scan rate on real hardware.
