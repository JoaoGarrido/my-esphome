# Bill of Materials — LED Strip Controller

| #   | Component                    | Description                                   | Qty | Notes                                                                           |
| --- | ---------------------------- | --------------------------------------------- | --- | ------------------------------------------------------------------------------- |
| 1   | ESP32-C6-DevKitC-1           | Espressif development board with ESP32-C6 SoC | 1   | Thread (OpenThread) FTD (router), Wi-Fi disabled                                |
| 2   | LM2596 buck converter module | Step-down DC-DC, 24V → 5V                     | 1   | Powers ESP32-C6 via 5V pin; set output to 5V before connecting                  |
| 3   | IRLB8721PbF                  | N-channel logic-level MOSFET (TO-220)         | 2   | One per LED channel (cold white GPIO4, warm white GPIO5); 30V, 62A, low Rds(on) |
| 4   | 100 Ω resistor               | Gate resistor                                 | 2   | Limits gate current; 1/4W                                                       |
| 5   | 10 kΩ resistor               | Gate pull-down resistor                       | 2   | Keeps MOSFET off when GPIO is floating                                          |

## Connections

### LED strip → MOSFETs (low-side switching)

| From           | To             | Notes                    |
| -------------- | -------------- | ------------------------ |
| 24V PSU +      | LED strip CW + | Cold white positive rail |
| 24V PSU +      | LED strip WW + | Warm white positive rail |
| LED strip CW − | MOSFET1 drain  | Cold white channel       |
| LED strip WW − | MOSFET2 drain  | Warm white channel       |
| MOSFET1 source | GND            | Common ground            |
| MOSFET2 source | GND            | Common ground            |
| 24V PSU −      | GND            | Common ground            |

### ESP32-C6 → MOSFET gates

| From         | To                   | Notes          |
| ------------ | -------------------- | -------------- |
| GPIO4        | 100 Ω → MOSFET1 gate | Cold white PWM |
| GPIO5        | 100 Ω → MOSFET2 gate | Warm white PWM |
| MOSFET1 gate | 10 kΩ → GND          | Pull-down      |
| MOSFET2 gate | 10 kΩ → GND          | Pull-down      |

### Power for ESP32-C6

| From             | To              | Notes                        |
| ---------------- | --------------- | ---------------------------- |
| 24V PSU +        | LM2596 Vin      | Buck converter input         |
| 24V PSU −        | LM2596 GND      |                              |
| LM2596 Vout (5V) | ESP32-C6 5V pin | Powers ESP32 via onboard LDO |
| LM2596 GND       | ESP32-C6 GND    | Common ground                |
