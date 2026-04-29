# Pico W Keypad + 12-LED Panel

Documentation-first repository structure for a Raspberry Pi Pico W project based on the provided Wokwi hardware diagram.

## Repository structure (MicroPython-oriented)

- `src/`
  - `diagram.json` — normalized copy of the provided Wokwi diagram.
  - `main.py` — expected location for your existing firmware logic (keep original content here).
- `lib/`
  - Optional MicroPython helper modules.
- `docs/`
  - `wiring.md` — complete wiring and GPIO map.
  - `architecture.md` — firmware/module architecture.
- `README.md`

> Note: No firmware logic was changed in this task. If you already have `main.py`, place it under `src/main.py` unchanged.

## Project overview

This design connects:
- One **4x4 membrane keypad** (8 GPIO lines)
- Twelve discrete LEDs (8 blue for numeric indicators + 4 red for A/B/C/D indicators)
- Current-limiting resistors for all LEDs
- Four 1k pull-up resistors for keypad row lines

The Pico W can read keypad events and drive the 12 LED outputs according to your existing main firmware logic.

## Features supported by this hardware

- 4x4 keypad matrix scanning (rows + columns)
- 12 independent LED indicators
- UART monitoring through `GP0/GP1` in simulation
- Designed for both Wokwi testing and real-board wiring

## Flash/run instructions

### Run in Wokwi
1. Create/open a Raspberry Pi Pico W project in Wokwi.
2. Use `src/diagram.json` content as your `diagram.json`.
3. Add your firmware as `main.py` (from your original source, unchanged).
4. Start simulation and use Serial Monitor for logs.

### Run on real Pico W (MicroPython)
1. Install the latest stable MicroPython UF2 for **Raspberry Pi Pico W**.
2. Mount Pico W as USB storage in BOOTSEL mode and copy UF2.
3. Copy firmware files:
   - `src/main.py` → board root as `main.py`
   - optional modules from `lib/`
4. Open serial REPL (115200 default) and reset.

## Wi-Fi notes

No Wi-Fi logic is present in the provided diagram data. If your `main.py` uses Wi-Fi:
- Keep credentials in a separate local file (for example `secrets.py`) not committed to git.
- Load credentials at runtime.
- Add `secrets.py` to `.gitignore`.

## Hardware reference

See:
- `docs/wiring.md` for full GPIO and component mapping
- `docs/architecture.md` for software structure recommendations
