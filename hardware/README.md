# Hardware and wiring

## Target hardware

- NodeMCU-32S based on the ESP32-WROOM
- Google AIY Voice HAT

> The following mapping documents the planned wiring from the project notes. It is not a
> tested PCB schematic or a production approval. Verify the board revision and signal
> directions before applying power for the first time.

## NodeMCU-32S ↔ Voice HAT

| NodeMCU-32S | Voice HAT physical pin | Function | Direction |
| --- | --- | --- | --- |
| GPIO26 | Pin 12 | I2S bit clock (`BCLK`) | ESP32 → HAT |
| GPIO25 | Pin 35 | I2S word clock (`LRCLK` / `WS`) | ESP32 → HAT |
| GPIO22 | Pin 40 | I2S data output (`DOUT`) | ESP32 → MAX98357A |
| GPIO34 | Pin 38 | I2S data input (`DIN`) | Microphone → ESP32 |
| GPIO27 | Pin 36 | Amplifier enable/shutdown control | ESP32 → HAT |
| 3V3 | Pin 17 | 3.3 V rail | Power |
| VIN / 5V | Pin 2 **or** 4 | HAT 5 V supply | Power |
| GND | Pin 6 | Common ground | Power |

## Names for firmware pin definitions

| Constant | GPIO | Note |
| --- | ---: | --- |
| `I2S_BCLK` | 26 | ESP32 output |
| `I2S_LRCLK` | 25 | ESP32 output |
| `I2S_DOUT` | 22 | Serial data to the amplifier |
| `I2S_DIN` | 34 | Input only; serial data from the microphone |
| `AMP_ENABLE` | 27 | Verify the active level for the board revision |

Both I2S data directions are used in this wiring. The driver design must separately validate
clock sharing, the full-duplex data path, and the microphone board's phase/slot settings.

## Safety and validation

- Make power connections with both boards unpowered.
- Use **only one** of physical pins 2 and 4 for the 5 V supply.
- Do not confuse 3.3 V signals with 5 V power; do not apply 5 V to GPIO pins.
- When using USB and external 5 V power together, check the NodeMCU board's power path.
- GPIO34 is an input-only pin; it cannot be used for amplifier control or data output.
- Before first power-up, check for shorts between VIN/5V and GND, and between 3V3 and GND.
- Validate the microphone, amplifier, and speaker independently before testing two-way audio.

## Planned technical outputs

- Schematics and wiring diagrams for the relevant board revisions
- Speaker power and power-supply budget
- Ground and power placement for noise/EMI control
- Enclosure, microphone opening, and speaker mounting
