# Wiring and GPIO Mapping (Raspberry Pi Pico W)

## Components list (derived from diagram)

- 1x Raspberry Pi Pico / Pico W-compatible board
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8x blue LEDs labeled `1..8`
  - 4x red LEDs labeled `A..D`
- 12x 220Ω resistors (`r1..r12`) for LED current limiting
- 4x 1kΩ resistors (`rp1..rp4`) used as keypad row pull-ups
- Shared ground return for all LED cathodes

## Keypad GPIO mapping

| Keypad signal | Pico W GPIO | Notes |
|---|---:|---|
| C4 | GP16 | Matrix column |
| C3 | GP17 | Matrix column |
| C2 | GP18 | Matrix column |
| C1 | GP19 | Matrix column |
| R4 | GP20 | Matrix row + 1k pull-up to 3V3 |
| R3 | GP21 | Matrix row + 1k pull-up to 3V3 |
| R2 | GP22 | Matrix row + 1k pull-up to 3V3 |
| R1 | GP26 | Matrix row + 1k pull-up to 3V3 |

## LED GPIO mapping

| LED label | LED color | Pico W GPIO | Series resistor |
|---|---|---:|---|
| 1 | Blue | GP11 | 220Ω (`r8`) |
| 2 | Blue | GP10 | 220Ω (`r7`) |
| 3 | Blue | GP9  | 220Ω (`r6`) |
| 4 | Blue | GP8  | 220Ω (`r5`) |
| 5 | Blue | GP7  | 220Ω (`r4`) |
| 6 | Blue | GP6  | 220Ω (`r3`) |
| 7 | Blue | GP5  | 220Ω (`r2`) |
| 8 | Blue | GP4  | 220Ω (`r1`) |
| A | Red | GP3  | 220Ω (`r9`) |
| B | Red | GP2  | 220Ω (`r10`) |
| C | Red | GP28 | 220Ω (`r11`) |
| D | Red | GP27 | 220Ω (`r12`) |

All LED cathodes connect to GND.

## Other signal usage

| Pico W pin | Usage |
|---|---|
| GP0 | UART TX to Wokwi serial monitor RX |
| GP1 | UART RX to Wokwi serial monitor TX |
| 3V3 | Pull-up rail for keypad row resistors (`rp1..rp4`) |
| GND | Common ground for LEDs |

## Assumptions and cautions

- Diagram uses `wokwi-pi-pico`; this documentation targets **Pico W** and is pin-compatible for listed GPIOs.
- 1k row pull-ups are external in diagram; if firmware also enables internal pull resistors, behavior should still be deterministic but validate debounce timing.
- GP26/GP27/GP28 are ADC-capable pins; using them as digital GPIO is valid.
