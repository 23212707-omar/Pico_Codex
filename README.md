# Pico W Environmental Monitor (DHT22 + I2C LCD1602)

This repository keeps a clean, documentation-first structure for a Raspberry Pi Pico W project.
The repository layout remains:

- `src/` — firmware entrypoint and simulation artifacts
- `lib/` — optional MicroPython support modules
- `docs/` — hardware and architecture documentation

> Core firmware behavior is preserved: no application logic changes are introduced by this documentation refresh.

## Project overview

Based on the requested hardware interpretation, this project is an **environmental monitoring system** using:

- Raspberry Pi Pico W (RP2040 + Wi-Fi)
- DHT22 temperature/humidity sensor
- 1602 LCD with I2C PCF8574 backpack

The Pico W reads temperature/humidity from DHT22 and displays values on the I2C LCD. Wi-Fi may be used by your existing `main.py` for logging/telemetry.

## Repository structure

- `src/main.py` — existing MicroPython firmware entrypoint (keep unchanged)
- `src/diagram.json` — provided Wokwi JSON snapshot
- `lib/` — reusable helper modules (optional)
- `docs/wiring.md` — GPIO and wiring reference for this hardware description
- `docs/architecture.md` — module and runtime-flow overview

## Hardware summary (documentation target)

- **LCD1602 (I2C via PCF8574):**
  - `SDA -> GP0`
  - `SCL -> GP1`
  - `VCC -> VBUS (5V)`
  - `GND -> GND`
- **DHT22:**
  - `DATA -> GP15`
  - `VCC -> 3V3`
  - `GND -> GND`

## Run in Wokwi

1. Create a new Raspberry Pi Pico W project in Wokwi.
2. Add the required parts:
   - Pico W
   - DHT22
   - LCD1602 + I2C backpack (PCF8574)
3. Wire the project exactly as listed in `docs/wiring.md`.
4. Copy your existing firmware into `src/main.py` (unchanged logic).
5. Start simulation and monitor output.

## Run on real hardware (MicroPython)

1. Flash the Pico W with MicroPython UF2.
2. Copy your firmware files to the board:
   - `src/main.py` as `main.py`
   - optional modules from `lib/`
3. Wire DHT22 and I2C LCD per `docs/wiring.md`.
4. Reset the board and verify LCD updates/sensor reads.

## Wi-Fi credentials handling

If your existing firmware uses Wi-Fi:

- Store credentials in a separate `secrets.py` file.
- Keep `secrets.py` out of git (add to `.gitignore`).
- Never hardcode credentials in documentation or source history.

## Important note about source artifacts

The committed `src/diagram.json` still reflects the original provided Wokwi JSON snapshot (keypad + LED matrix style wiring). This README and `docs/wiring.md` are intentionally updated to the requested **environmental monitor** mapping target.
