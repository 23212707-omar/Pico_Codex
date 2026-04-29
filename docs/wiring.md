# Wiring and GPIO Mapping (Raspberry Pi Pico W)

## Documentation target

This wiring document is aligned to the requested environmental monitoring hardware description:

- LCD1602 over I2C (PCF8574 adapter)
- DHT22 temperature/humidity sensor
- Raspberry Pi Pico W

## Components list

- 1x Raspberry Pi Pico W
- 1x DHT22 sensor
- 1x 1602 LCD with I2C backpack (PCF8574)
- Jumper wires
- USB power/programming cable

## GPIO mapping table

| Module | Signal | Pico W pin | Notes |
|---|---|---|---|
| LCD1602 (I2C) | SDA | GP0 | I2C data line |
| LCD1602 (I2C) | SCL | GP1 | I2C clock line |
| LCD1602 (I2C) | VCC | VBUS (5V) | Power for LCD backpack |
| LCD1602 (I2C) | GND | GND | Common ground |
| DHT22 | DATA | GP15 | One-wire digital data |
| DHT22 | VCC | 3V3 | Sensor supply |
| DHT22 | GND | GND | Common ground |

## Electrical and integration notes

- Ensure **common ground** between Pico W, DHT22, and LCD module.
- DHT22 data line commonly uses a pull-up resistor in physical builds (often 4.7k–10k to 3.3V). Some breakout modules already include this.
- The LCD I2C backpack address is often `0x27` or `0x3F`; confirm in your firmware/config.
- GP0/GP1 are assigned to I2C here as requested; avoid reusing them for UART in this wiring profile.

## Wokwi build checklist

1. Place Pico W, DHT22, and I2C LCD1602 parts.
2. Wire SDA/SCL to GP0/GP1.
3. Wire DHT22 data to GP15.
4. Power LCD from VBUS (5V) and sensor from 3V3.
5. Verify all grounds are tied together.

## Consistency note

The repository includes an earlier `src/diagram.json` snapshot with different parts and net assignments. For this iteration, follow the mapping in this file as the authoritative target requested by the user.
