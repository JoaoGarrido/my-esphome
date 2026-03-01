# Bill of Materials — Temperature & Humidity Sensor

| # | Component | Description | Qty | Notes |
|---|-----------|-------------|-----|-------|
| 1 | ESP32-C6-DevKitC-1 | Espressif development board with ESP32-C6 SoC | 1 | Thread (OpenThread) MTD, Wi-Fi disabled |
| 2 | SHT41 | Sensirion temperature & humidity sensor | 1 | I2C, SDA: GPIO21, SCL: GPIO22 |
| \*3 | AAA battery | NiMH or alkaline — see notes | 3 | Recommended: Panasonic Eneloop (BK-4MCCE) |
| \*4 | AAA × 3 battery holder | 3-cell AAA holder with leads or JST connector | 1 | Voltage range: 3.0–3.6V (Eneloop) or 3.3–4.5V (alkaline) |
| \*5 | MCP1703-3302E | 3.3V LDO voltage regulator (TO-92) | 1 | Ultra-low dropout ~100mV, quiescent ~2 µA, max 250mA |

\* Only required if building a battery powered device.

## Connections

### SHT41 → ESP32-C6

| SHT41 Pin | ESP32-C6 Pin |
|-----------|-------------|
| VCC       | 3.3V         |
| GND       | GND          |
| SDA       | GPIO21       |
| SCL       | GPIO22       |

## Power circuit

### Battery powered

| From | To | Notes |
|------|----|-------|
| Battery holder + | MCP1703 Vin | 3.0–4.5V depending on battery type and charge state |
| MCP1703 Vout | ESP32-C6 3V3 pin | Bypasses onboard LDO |
| Battery holder − | ESP32-C6 GND | Common ground |

### Mains powered

Connect a USB power supply to the USB JTAG of the ESP32-C6.
