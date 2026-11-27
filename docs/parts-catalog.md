# Chord: Parts and Modules Catalog

Candidate parts found during the design review (Nov 2026), grouped by area and tagged with where each one would plug in under the [expansion system](expansion-system.md).

- **Prices** are approximate US unit prices. A **?** means the price or status could not be confirmed at the time. Check stock, lifecycle and FCC IDs (fccid.io) before ordering anything.
- **Fits** uses the v0.2 layout: radios go in the **radio head**, wired tools in the **tool bay** (Bay B), receive-only modules in a **bay**, I2C boards on a **Qwiic pod**, big or hot gear on the **dock**.
- **LAB** items need the acceptable-use policy, training and supervision. **Training** items need training first.
- **Rejected** items are struck through and kept so nobody re-proposes them without reading why.

| Area | Entries |
|---|---|
| [Beginner pods (zero solder)](#beginner-pods-zero-solder) | 25 |
| [Radios, GNSS and IR](#radios-gnss-and-ir) | 24 |
| [Audio, haptics and receivers](#audio-haptics-and-receivers) | 23 |
| [Power and bench measurement](#power-and-bench-measurement) | 20 |
| [Compute, co-processors and cameras](#compute-co-processors-and-cameras) | 23 |
| [Identity and security tools](#identity-and-security-tools) | 23 |
| [Field, automotive and industrial](#field-automotive-and-industrial) | 21 |
| [Connectors, displays and input](#connectors-displays-and-input) | 25 |
| [Software and app-only features](#software-and-app-only-features) | 18 |
| [Expansion standards and precedents](#expansion-standards-and-precedents) | 20 |
| **Total** | **222** |

## Beginner pods (zero solder)

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| Adafruit VL53L4CD (5396) | Distance 1–1300 mm: tape measure, theremin | Qwiic, 0x29 | $14.95 | Qwiic pod | Default starter pick | [adafruit.com](https://www.adafruit.com/product/5396) |
| Adafruit LTR390 (4831) | UV index + ambient light | Qwiic, 0x53 | $4.95 | Qwiic pod | Sits inside the 0x50–0x57 ID range, so it needs its own mux segment. Default starter pick | [mouser.com](https://www.mouser.com/ProductDetail/485-4831) |
| Adafruit VEML7700 (4162) | Lux meter | Qwiic, 0x10 | $4.95 | Qwiic pod | Same address as the PA1010D GPS | [mouser.com](https://www.mouser.com/ProductDetail/485-4162) |
| Adafruit BME688 (5046) | Temperature, humidity, pressure, gas | Qwiic, 0x76/77 | $19.95 | Qwiic pod | Earned upgrade or at-cost add-on | [adafruit.com](https://www.adafruit.com/products/5046) |
| Arduino Modulino nodes | Thermo, Distance, Movement, Knob, Buzzer, Pixels, Buttons | Qwiic | $6.50–11.80 | Qwiic pod | Arduino and MicroPython libraries | [cnx-software.com](https://www.cnx-software.com/2025/05/23/arduino-launches-nano-connector-carrier-working-with-seven-modulino-expansion-nodes/) |
| Adafruit STCC4 + SHT41 (6478) | Lower-cost CO₂ + temp/humidity | Qwiic | $27.50 | Qwiic pod | New part; accuracy vs NDIR not verified | [learn.adafruit.com](https://learn.adafruit.com/adafruit-stcc4-and-sht41-co2-temperature-humidity-sensor?view=all) |
| Adafruit SCD-41 (5190) | True NDIR CO₂ | Qwiic | $49.95 | Qwiic pod | Lending library | [mouser.com](https://www.mouser.com/ProductDetail/485-5190) |
| SparkFun ENS160 (SEN-20844) | eCO₂, TVOC, air-quality index | Qwiic | $24.95 | Qwiic pod | BME280 combo board $39.95 | [sparkfun.com](https://www.sparkfun.com/sparkfun-indoor-air-quality-sensor-ens160-qwiic.html) |
| Adafruit SGP41 | VOC + NOx index | Qwiic | $19.95 | Qwiic pod | Needs temp/humidity compensation | [learn.adafruit.com](https://learn.adafruit.com/adafruit-sgp41-multi-pixel-gas-sensor-breakout) |
| Adafruit PMSA003I (4632) | PM1 / PM2.5 / PM10 | Qwiic | $44.95 | Dock | Has a fan, so desk use. Lending library | [adafruit.com](https://www.adafruit.com/product/4632) |
| Sensirion SEN66 + Adafruit SEN6x (6331) | PM, CO₂, VOC, NOx, temp/humidity in one | Qwiic | ~$65–95 + $5 ? | Dock | Desk air station. Lending library | [learn.adafruit.com](https://learn.adafruit.com/adafruit-sen6x-breakout) |
| Adafruit AS7341 (4698) | 10-channel light spectrometer | Qwiic, 0x39 | $18.95 | Qwiic pod | Same address as APDS9960 | [adafruit.com](https://www.adafruit.com/products/4698) |
| Adafruit APDS9960 (3595) | Gesture, proximity, RGB | Qwiic, 0x39 | ~$7.50 ? | Qwiic pod | Same address as AS7341 | [octopart.com](https://octopart.com/part/adafruit-industries/3595) |
| Adafruit LSM6DSOX + LIS3MDL (4517) | Raw 9-DoF IMU for DSP lessons | Qwiic | $19.95 | Qwiic pod |  | [adafruit.com](https://www.adafruit.com/products/4517) |
| Adafruit BNO085 (4754) | 9-DoF with on-chip sensor fusion | Qwiic | $29.50 | Qwiic pod | Lending library | [adafruit.com](https://www.adafruit.com/products/4754) |
| VL53L5CX (Adafruit 6503 / SparkFun SEN-18642) | 8×8 depth map, gestures | Qwiic, 0x29 | $19.95 / $32.50 | Qwiic pod | Same address as VL53L4CD | [adafruit.com](https://www.adafruit.com/product/6503) |
| Adafruit AMG8833 (3538) / Grove MLX90641 | 8×8 or 16×12 thermal | Qwiic / Grove | $44.95 / ~$45–65 | Qwiic pod | Grove needs an adapter cable | [adafruit.com](https://www.adafruit.com/product/3538) |
| Adafruit MLX90640 (4407 / 4469) | 32×24 thermal camera, 55° or 110° | Qwiic | $74.95 | Qwiic pod | The library's biggest 'wow' item | [adafruit.com](https://www.adafruit.com/product/4407) |
| SparkFun Pulse Oximeter (SEN-15219) | Heart rate + SpO₂ | Qwiic + reset and MFIO lines | $48.95 | Bay | Not a medical device; data stays on the badge. 12-week lead at DigiKey | [sparkfun.com](https://www.sparkfun.com/sparkfun-pulse-oximeter-and-heart-rate-sensor-max30101-max32664-qwiic.html) |
| AS3935 lightning detector | Storm distance | I2C or SPI + IRQ | ~£18.49 / $34.95 | Bay | SparkFun Qwiic version discontinued and needed an IRQ anyway | [sparkfun.com](https://www.sparkfun.com/sparkfun-lightning-detector-as3935.html) |
| DFRobot Gravity Geiger (SEN0463) | Radiation counts per minute | Pulse on a GPIO | $60 | Dock | Teaching grade. Lending library; tube is too tall for a bay | [dfrobot.com](https://www.dfrobot.com/product-2547.html) |
| Adafruit STEMMA soil sensor (4026) | Soil moisture + temperature | I2C on JST-PH | $7.50 | Qwiic pod | Needs a PH-to-SH cable | [adafruit.com](https://www.adafruit.com/products/4026) |
| Adafruit NeoKey 1×4 QT (4980) | Four macro keys with RGB | Qwiic | $9.95 | Qwiic pod | Switches not included | [adafruit.com](https://www.adafruit.com/product/4980) |
| Adafruit IS31FL3741 13×9 RGB matrix (5201) | LED matrix display | Qwiic | $14.95 | Qwiic pod | Budget its current | adafruit.com |
| Adafruit PCA9548 mux (5626) + QT cables | Resolves address clashes, links pods | Qwiic | ~$9 / $0.95 | Qwiic pod | Grove and M5 units need a 5 V converter | [jameco.com](https://www.jameco.com/z/5626-Adafruit-Industries-Adafruit-Pca9548-8-Channel-Stemma-QT-Qwiic-I2C-Multiplexer-Tca9548A-Compatible_2525871.html) |

## Radios, GNSS and IR

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| Seeed Wio-SX1262 | 915 MHz LoRa for Meshtastic | SPI + BUSY/DIO1 | $5.95 | Radio head | FCC Z4T-WIO-SX1262. Flagship earned upgrade | fcc.report |
| Seeed XIAO ESP32S3 + Wio-SX1262 kit | Complete Meshtastic node, talks to the badge over UART | UART | ~$10 ? | Radio head | Disable its own BLE/Wi-Fi. Fallback if the S31 port slips | wiki.seeedstudio.com |
| Seeed Wio-SX1262-1W | 1 W LoRa | SPI | ? | Dock | Grant requires 20 cm separation: fixed repeater only | fccid.io |
| Heltec HT-RA62 | SX1262 at 21 dBm, US915 | SPI | ? | Radio head | Second source; grant 2A2GJ-HT-CT62 not verified | heltec.org |
| RAKwireless RAK3172 | STM32WL LoRaWAN, AT commands | UART | ? | Radio head | FCC 2AF6B-RAK3172 (verify); buy the FCC/IC variant | docs.rakwireless.com |
| Seeed Wio-LR1121 | LoRa on sub-GHz, 2.4 GHz and S-band | SPI | ? | Radio head · LAB | Grant lists only 908.4–920 MHz; treat other bands as not covered | fccid.io |
| Semtech LR2021 (Gen 4) | Next-gen multi-band LoRa | SPI | EVK ? | Dock | No module with an FCC ID yet. Watch list | semtech.com |
| ~~Ebyte E28-2G4M27SX~~ | 2.4 GHz LoRa at 27 dBm | SPI | ? | Rejected | FCC 2A8C3-E28-2G4M27SX; brings back 2.4 GHz coexistence problems. Skip v1 | fccid.io |
| TTM A1101R09C | CC1101 at 915 MHz | SPI | ? | Radio head · LAB | FCC X7J-A10040601; settings outside the tested modes fall outside the grant | ttm.com |
| NiceRF RF4463PRO-915 | Si4463 FSK/OOK sub-GHz | SPI | ? | Radio head · LAB | FCC 2AD66-915 | nicerf.com |
| Uncertified sub-GHz boards (generic CC1101 incl. 315/433, M5 CC1101, E22-900M22S, RFM69HCW Wing) | Cheap sub-GHz radios | SPI | $3–20 ? | Dock · LAB | No FCC grant found. Club-owned lab kits, never handed out | lcsc.com |
| Qorvo DWM3001C | UWB ranging and positioning | UART / SPI | $49.48 | Radio head · LAB | Handheld UWB may only transmit to an associated receiver (§15.519) | qorvo.com |
| Nordic nRF9151 | LTE-M / NB-IoT + GNSS + satellite NTN | UART | ? | Dock · LAB | Grant has a 20 cm condition; needs an IoT SIM | nordicsemi.com |
| Quectel BG95-M3 / SIMCom SIM7080G | LTE-M / NB-IoT modems | UART | ? | Dock · LAB | BG95 FCC XMR202010BG95M3 with carrier approvals | quectel.com |
| RockBLOCK 9603 / Myriota HyperPulse | Satellite messaging | UART / standalone | $299.95 / $199 | Dock · LAB | Swarm is dead (service ended March 2025) | sparkfun.com |
| SparkFun SAM-M10Q / MAX-M10S / NEO-M9N | u-blox GNSS | Qwiic / UART | $51.50 / $45.95 / $76.50 | Qwiic pod | Receive-only. SAM-M10Q (0x42) is the default GPS pod | sparkfun.com |
| Adafruit Mini GPS PA1010D (4415) | GNSS with patch antenna | Qwiic / UART, 0x10 | $29.95 | Qwiic pod | Receive-only; clashes with VEML7700 at 0x10 | [adafruit.com](https://www.adafruit.com/product/4415) |
| Waveshare LC76G / L76K | Cheapest multi-GNSS with antenna | UART + I2C / UART | $14.99 / $12.99 | Radio head | Receive-only; L76K lacks Galileo; GNSS with an antenna goes in a radio head (too tall for a bay) | waveshare.com |
| SparkFun GPS-RTK2 (ZED-F9P) / Quectel LC29H | Centimetre-level RTK | Qwiic / UART | $259.95 / ~$32–42 | Dock | Receive-only | sparkfun.com |
| ADSBee 1090 (m1090) | Open-source ADS-B aircraft receiver | UART | ? | Radio head | Receive-only | [github.com](https://github.com/CoolNamesAllTaken/adsbee) |
| dAISy HAT / dAISy 2+ | AIS ship tracking at 162 MHz | UART / USB | ~$79 / £113.90 | Dock | Receive-only | reach.dog |
| RTL-SDR Blog V4 | 24–1766 MHz SDR; decodes 315/433 fobs with rtl_433 | USB host | $34.95–39.95 | Dock | Receive-only hardware: the legal capture tool | rtl-sdr.com |
| TSOP38238 + 940 nm IR LED | IR remote learn and send | GPIO via RMT | <$2 ? | Core board | Not RF. Keep the blaster within eye-safety limits | adafruit.com |
| S31-WROOM-3 PCB antenna vs -3U u.FL | Antenna strategy | — | ? | Core board | -3U certified with one monopole; ship only granted antenna types, RP-SMA | documentation.espressif.com |

## Audio, haptics and receivers

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| Everest ES8388 codec | Stereo codec, 40 mW headphone, headset mic + radio line-in | I2S + I2C | $1.10 ($0.57 @500) | Core board | Replaces the obsolete WM8960. Hardware-verified in esp_codec_dev | [lcsc.com](https://www.lcsc.com/product-detail/C365736.html) |
| NS4150B + 1 W 8 Ω speaker | Speaker output from the codec | Analog | ? | Core board | Same pairing M5Stack ships. Peaks ~0.5 A: duck volume during TX | [docs.m5stack.com](https://docs.m5stack.com/en/products/sku/A149) |
| Nuvoton NAU88C22YG | One-chip codec with headphone, 1 W speaker, mic preamps | I2S + I2C | ? | Core board | No esp_codec_dev driver; we'd port one | [nuvoton.com](https://www.nuvoton.com/export/resource-files/DS_NAU88C22_DataSheet_EN_Rev1.1.pdf) |
| TI TLV320AIC3111 | Codec + 1.29 W class-D + miniDSP | I2S + I2C | ? | Core board | Active; no esp_codec_dev driver | [ti.com](https://ti.com/product/TLV320AIC3111) |
| ~~Cirrus WM8960~~ | The round-2 codec pick | — | — | Rejected | Obsolete, last-time-buy July 2022. Retracted | [octopart.com](https://octopart.com/part/cirrus-logic/WM8960CGEFL%2FRV) |
| TDK T5838 PDM mic | Wake-on-sound at ~20 µA | PDM | ? | Core board | Only TDK's flex eval board; needs S31 PDM RX | [invensense.tdk.com](https://invensense.tdk.com/products/T5838) |
| ~~TDK ICS-43434 / INMP441~~ | The I2S mics in the original spec | I2S | — | Rejected | ICS-43434 EOL (LTB 15 Jun 2026); INMP441 eval discontinued | [digikey.com](https://www.digikey.com/en/products/detail/tdk-invensense/ICS-43434/6140298) |
| MSM261S4030H0 (DFRobot SEN0526) | Cheap I2S mic for dev kits | I2S | ? | Dock | Sources disagree on port side | [wiki.dfrobot.com](https://wiki.dfrobot.com/SKU_SEN0526_Fermion_I2S_MEMS_Microphone) |
| TI DRV2605L (Adafruit 2305) | Haptic effects library for vibration motors | Qwiic | ~$8 ? | Qwiic pod | Starter pick; moves onto the base at Rev B | [adafruit.com](https://www.adafruit.com/products/2305) |
| SparkFun Qwiic Haptic DA7280 (ROB-17590) | LRA driver with motor on board | Qwiic | $11.50 | Qwiic pod | On backorder | [sparkfun.com](https://www.sparkfun.com/sparkfun-qwiic-haptic-driver-da7280.html) |
| Skyworks Si4732-A10 | AM/FM/LW/SW receiver, SSB by patch | I2C + analog to RADIO_IN | ? | Radio head | Receive-only. Keep the third-party SSB patch out of our repo. Open ATS-Mini firmware to port | [esp32-si4732.github.io](https://esp32-si4732.github.io/ats-mini/) |
| RDA5807M (ScoutMakes STEMMA QT, Grove) | FM radio with RDS song text | I2C | ? | Qwiic pod | Receive-only | [learn.adafruit.com](https://learn.adafruit.com/scoutmakes-fm-radio-board-stemma-i2c) |
| Skyworks Si4707 | NOAA weather radio + emergency-alert decode | I2C | ? | Radio head | SparkFun board retired; chip-down only | [learn.sparkfun.com](https://learn.sparkfun.com/tutorials/si4707-hookup-guide) |
| ~~Skyworks Si4713~~ | FM transmitter + RDS | I2C | — | Rejected | No FCC ID; breakout reportedly gone. Don't ship | [forum.arduino.cc](https://forum.arduino.cc/t/new-software-for-si4713-fm-transmitter-with-rds/1433391) |
| SA818-V/U / DRA818 | 0.5–1 W 2 m / 70 cm FM for APRS | UART + analog + PTT | ? | Radio head · LAB | Ham licence required; no FCC ID found; needs filtering. Licensed members only | [hackaday.io](https://hackaday.io/project/174358) |
| M5Stack Unit Synth U178 (SAM2695) | 64-voice General MIDI synth + speaker | UART 31250 | ? | Qwiic pod | Use Qwiic port 2 in UART mode | [docs.m5stack.com](https://docs.m5stack.com/en/unit/Unit_Synth) |
| M5Stack Atomic Voice Base (A149) | ES8311 + mic + amp + 1 W speaker | I2S + I2C | $5.95 | Dock | Semester-0 voice dev kit | [switch-science.com](https://www.switch-science.com/products/10193) |
| Adafruit TLV320DAC3100 (6309) | DAC + headphone + 1.6 W speaker | I2S + I2C | $6.95 | Dock | Dev kit | [adafruit.com](https://www.adafruit.com/product/6309) |
| MAX98357A (SparkFun / Adafruit stereo) | 3.2 W I2S class-D amp | I2S | $7.50 / $9.95 | Dock | Desk speaker; the base codec drives a speaker already | [sparkfun.com](https://www.sparkfun.com/sparkfun-i2s-audio-breakout-max98357a.html) |
| Everest ES7210 | 4-channel mic ADC for arrays and direction finding | TDM + I2C | ? | Dock | No breakout found | [components.espressif.com](https://components.espressif.com/components/espressif/esp_codec_dev/) |
| Analog Devices ADAU1701 | SigmaDSP EQ and crossover | I2S + I2C | ? | Dock | LCSC flags it not for new designs | [analog.com](https://www.analog.com/en/products/adau1701.html) |
| USB-MIDI / BLE-MIDI | Badge as a MIDI controller | USB / BLE | $0 | App (no hardware) | TinyUSB / NimBLE |  |
| Goertzel tone decoding | DTMF, CTCSS and alert tones in firmware | — | $0 | App (no hardware) | Replaces an MT8870 chip |  |

## Power and bench measurement

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| TPS2121 mux + VIN_EXT path | Lets every power accessory feed the badge; USB-C wins | Power | $1.50 ? | Core board | 2.8–22 V priority mux into the BQ24074 | ti.com |
| MAX17055 fuel gauge | Real per-app current from a sense resistor | I2C | $2.50 ? | Core board | Replaces MAX17048 so runtime per mode is measured | analog.com |
| Booster cover (BQ25895 + 403450 cell) | About +40% runtime, own USB-C charging | Power, I2C | $12 BOM ? | Power cover | Protected, UN38.3 cell. Prototype with PowerBoost 1000C | ti.com |
| Qi cover (BQ51013B or P9222-R + coil) | Drop it on a charging pad | Power | $8 BOM ? | Power cover | 5 W class; ferrite sheet between coil and cell | ti.com |
| Solar cover (6 V panel) | Field top-up through the charger's input regulation | Power | $6 ? | Power cover | 0.3–0.5 W in full sun, mW indoors | adafruit.com |
| BQ25570 / SPV1050 | Microwatt harvesting into a supercap | Power | $4 ? | Qwiic pod | For self-powered sensor nodes, not the badge cell | ti.com |
| CN3791 MPPT charger | 4 A solar charging for a separate field pack | Power | $3 ? | Dock | A second charger, never on the badge cell | consonance-elec.com |
| HUSB238 / STUSB4500 / CH224K | Turn any USB-C charger into a 5–20 V supply | I2C or resistor-set | $2–15 ? | Qwiic pod · LAB | Output to screw terminals, never into the badge | adafruit.com |
| AP33772S PPS sink (PocketPD-style) | 3.3–21 V in 20 mV steps with current limit | I2C | $3 IC ? | Tool bay (Bay B) · LAB | Needs a PPS-capable charger | diodes.com |
| TPS55289 behind a PD sink | Constant-voltage / constant-current bench supply | I2C | $4 IC ? | Dock · LAB | ~1–22 V, 30 W; too hot for a pocket | ti.com |
| ~~IP5306 / IP5328P / IP2366~~ | Power-bank output | — | $1–3 ? | Rejected | Thin datasheets, light-load auto-off, and a 7.4 Wh badge is a poor phone charger | injoinic.com |
| INA228 (Adafruit); INA219 / INA260 / INA3221 | 85 V, 20-bit voltage, current, energy | Qwiic | $6–15 ? | Qwiic pod | Starter pick: profile your own badge | adafruit.com |
| Inline USB-C analyzer (INA228 + FUSB302B) | VBUS power meter + USB-PD sniffer | I2C | $10 BOM ? | Tool bay (Bay B) | VBUS never touches badge rails; Twonkie is the reference | onsemi.com |
| Nordic PPK2 | Power profiler from 200 nA to 1 A | USB host | $99 ? | Dock | The badge's USB host could drive it | nordicsemi.com |
| CurrentRanger / uCurrent Gold | Low-burden current amplifier, nA to mA | Analog | $80–150 ? | Tool bay (Bay B) | CurrentRanger is open hardware | lowpowerlab.com |
| Electronic load (MCP4725 + MOSFET + INA228) | Constant-current load for battery tests | I2C | $25 BOM ? | Dock · LAB | Dissipates watts: fan and NTC cutoff | adafruit.com |
| ADS1115 / NAU7802 (Qwiic Scale) | Simple multimeter or 24-bit load-cell input | Qwiic | $10–15 ? | Qwiic pod | Up to 30 V through a divider, never mains | sparkfun.com |
| ADS1220 (ProtoCentral) / ADS131M04 | 24-bit RTD/bridge or 4-channel simultaneous capture | SPI | $5–20 ? | Bay | No ADS131M04 breakout found | ti.com |
| RP2350 scope front end (Scoppy-style) | ~500 kS/s oscilloscope reusing the logic analyzer | SPI / USB | $15 BOM ? | Tool bay (Bay B) · LAB | Probe ground is the laptop's ground; 30 V max | tindie.com |
| AD9833 / AD9850 DDS | Sine/square output to 12.5 MHz (AD9850 ~40 MHz) | SPI | $5–10 ? | Tool bay (Bay B) · LAB | Wired output only; with an antenna it's a transmitter | analog.com |

## Compute, co-processors and cameras

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| ESP32-C5-WROOM-1U-N8R8 | 5 GHz Wi-Fi 6 scanning (the S31 is 2.4 GHz only) | UART / SPI via ESP-Hosted | $5.47 ($4.14 @100) | Radio head · LAB | C5-MINI-1 has a 5 GHz FCC cert; check the WROOM ID. 20-week lead. Monitor mode by default. Moved from bay to rail in round 4 | [digikey.com](https://www.digikey.com/en/products/detail/espressif-systems/esp32-c5-wroom-1u-n8r8/27566801) |
| ~~ESP32-C6-MINI-1~~ | Second 2.4 GHz radio for sniffing | UART / SPI | ~$3–4 ? | Rejected | FCC 2AC7Z-ESPC6MINI1. Dropped: duplicates the S31 and adds a transmitter 2 cm from its antenna | [espressif.com](https://www.espressif.com/sites/default/files/ESP32-C6-MINI-1%20FCC%20Certification.pdf) |
| ~~ESP32-H2-MINI-1~~ | 802.15.4 + BLE | UART | ? | Rejected | Duplicates S31 radios; no US grant found | espressif.com |
| Waveshare ESP32-P4-WIFI6 | MIPI camera and display desk station | USB / UART | $13.99 | Dock | Radio is a C6; board FCC not verified | [waveshare.com](https://www.waveshare.com/esp32-p4-wifi6.htm?sku=32020) |
| Nordic nRF52840 Dongle | Nordic BLE sniffer into Wireshark | USB | ~$10 ? | Dock · LAB | Sniffle does not run on it | [docs.nordicsemi.com](https://docs.nordicsemi.com/r/bundle/nrfutil/page/nrfutil-ble-sniffer/guides/requirements.html/supported-development-kits-and-dongles) |
| TI CC1352P / CC2652P (CatSniffer V3, SONOFF dongle) | Sniffle BLE 5 sniffer, Zigbee and Thread | UART / USB | ? | Dock · LAB | Supported Sniffle hardware; FCC not verified | [github.com](https://github.com/nccgroup/sniffle) |
| RAKwireless RAK4631 | Complete Meshtastic node (nRF52840 + SX1262) | UART / BLE | $17.99 | Radio head | Runs on its own; FCC ID not found. Also good as fixed campus repeaters | [store.rakwireless.com](https://store.rakwireless.com/products/rak4631-lpwan-node) |
| Seeed XIAO nRF54L15 | BLE 6.0, Thread, Matter, Zigbee; Zephyr teaching board | UART / I2C | $9.90 | Radio head | It transmits, so rail only. FCC not verified | [hackster.io](https://www.hackster.io/news/seeed-studio-packs-ble-6-0-thread-matter-zigbee-and-more-into-the-new-xiao-nrf54l15-429ae1490e7a) |
| Nordic nRF5340 (Raytac MDBT53) | LE Audio / Auracast companion | I2S + UART | ? | Radio head | Needs I2S, which CMI v0.1 doesn't carry. Open question | nordicsemi.com |
| Raspberry Pi RP2350 / Pico 2 | PIO logic analyzer, SWD debug probe, UART bridge | SPI / UART + probe header | ~$1 chip / ~$5 Pico 2 ? | Tool bay (Bay B) | No radio. Carries its own USB-C for PulseView | raspberrypi.com |
| Lattice iCE40UP5K (pico-ice / pico2-ice) | FPGA with open toolchain: glitch timing, fast capture | SPI | ? | Tool bay (Bay B) · LAB | Needs a 1.2 V core rail and config flash | tinyvision.ai |
| Sipeed Tang Nano 9K (GW1NR-9) | Cheap bench FPGA with HDMI | USB | ~$15–20 ? | Dock | Vendor tools closed; open flow partial | sipeed.com |
| WCH CH32V003 | Optional 'smart ID' on a module: local GPIO, ADC, sequencing | ID bus I2C | ~$0.10–0.15 ? | Part used on modules | Emulates the same EEPROM header; treated as untrusted; ~+$0.20/module at 100 incl. flashing | wch-ic.com |
| WIZnet W5500 / W6100 | Wired Ethernet with hardware TCP/IP | SPI | ~$3–4 ? | Dock | ESP-IDF has a W5500 driver | wiznet.io |
| ~~Analog Devices MAX3421E~~ | SPI USB host, full speed | SPI | ? | Rejected | Not needed: the S31's USB port can already be a host | analog.com |
| Microchip USB2514B | 4-port USB 2.0 hub | USB HS | ~$2 ? | Dock | The dock must supply 5 V | microchip.com |
| DVP cameras (OV3660, SC101IOT, OV2640, OV5640, GC0308) | Photos, QR codes, vision with the S31's JPEG engine | 8-bit DVP + SCCB, ~13 GPIO | ~$5–15 ? | Dock | Uses every spare pin, so dock or board variant. Needs a privacy policy | [developer.espressif.com](https://developer.espressif.com/workshops/introduction-to-esp32-s31-with-vision/overview-soc/) |
| Seeed Grove Vision AI V2 (Himax WE2) | On-module person and object detection | I2C / UART | ~$26 ? | Qwiic pod | Uses no S31 pins; badge only receives results | seeedstudio.com |
| Canaan K230 (CanMV-K230) | Linux-class RISC-V with NPU | USB / UART | ? | Dock | Too big for the pocket | canaan.io |
| ~~Winbond W25N01GV~~ | 128 MB SPI NAND | SPI | ? | Rejected | microSD and 16 MB flash already cover it | winbond.com |
| Fujitsu MB85RC256V FRAM (Adafruit) | 32 KB memory with unlimited writes for logs | I2C | ~$10 ? | Qwiic pod |  | adafruit.com |
| Micro Crystal RV-3028-C7 | ~45 nA clock that survives the hard-off switch | I2C | ~$3 ? | Core board | Keeps TOTP and logs correct. Needs a backup cap | sparkfun.com |
| S31 PARLIO + RMT + PCNT | 8-channel logic capture, IR, frequency counter | Built in | $0 | App (no hardware) | Needs a protected probe front-end cartridge | [esp32-s31.espressif.com](https://esp32-s31.espressif.com/en/docs/6-Pinout%20%26%20IO%20Introduction/pinout-and-io-allocation) |

## Identity and security tools

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| Microchip ATECC608B | Secure element; keys never leave the chip | I2C (private bus) | ~$0.70 ? | Core board | Signed meeting check-in; no module ever touches its bus | microchip.com |
| NXP SE050 (OM-SE050ARD) | Higher-assurance key store | I2C | ~$10 kit ? | Bay | Provisioning practice | nxp.com |
| Infineon OPTIGA Trust M (Shield2Go) | Secure element alternative, attestation labs | I2C | ~$8 ? | Bay |  | infineon.com |
| Tropic Square TROPIC01 | Open, auditable secure element | SPI | ? | Bay | Verify stock | tropicsquare.com |
| Adafruit ST25DV16K (4701) | Tap the badge to a phone for check-in | I2C + 13.56 MHz passive tag | ~$3.95 | Qwiic pod | Passive tag; zero offensive capability. Starter pick | [adafruit.com](https://www.adafruit.com/product/4701) |
| Raspberry Pi debugprobe | SWD/UART probe for secure-boot lessons | USB / SWD | ~$12 | Qwiic pod |  |  |
| M5Stack RFID Unit 2 (WS1850S) | Read and write your own 13.56 MHz tags | I2C | ~$4.95 | Qwiic pod · training | Reader transmits at 13.56 MHz; no FCC ID | [shop.m5stack.com](https://shop.m5stack.com/products/rfid-unit-2-ws1850s) |
| PN532 (Adafruit / Elechouse) | 13.56 MHz reader/writer, NDEF | I2C / SPI / UART | ~$40 ? | Qwiic pod · training | Emulation-capable: training gate | adafruit.com |
| SparkFun Qwiic RFID (ID-12LA) | 125 kHz read-only tag ID | Qwiic | $23.50 / $49.95 kit | Qwiic pod · training | Read-only means lower risk | [sparkfun.com](https://www.sparkfun.com/products/15191) |
| ST ST25R3916B (X-NUCLEO-NFC08A1 / NFC click) | High-performance reader incl. ISO 15693 | SPI / I2C | ~$30 ? | Bay · training | ST25R3918 is a reduced variant | [st.com](https://www.st.com/en/evaluation-tools/x-nucleo-nfc08a1.html) |
| NXP PN7160 | NCI reader controller | I2C / SPI | ? | Bay · training | Replaces PN7150, which is not for new designs | [nxp.com](https://www.nxp.com/products/rfid-nfc/nfc-hf/nfc-readers/high-performance-nfc-controller-with-integrated-firmware-for-smart-devices:PN7150) |
| NXP MFRC522 module | Cheap 13.56 MHz reader | SPI | ~$3 ? | Qwiic pod · training | Near end of life: labs only |  |
| 1-Wire iButton (DS9092 + DS1990A) | Contact token read and compare | 1-Wire | ~$5 ? | Qwiic pod · training |  | analog.com |
| NXP TDA8035 | ISO 7816 contact smartcard interface | SPI / UART | ? | Bay · training | Own or blank cards only | nxp.com |
| Tigard | Open JTAG/SWD/UART/SPI debug probe | USB | ~$40 | Dock · training |  | 1bitsquared.com |
| Bus Pirate 5 / 6 | Bus explorer, flash programmer | USB | ~$30–50 ? | Dock · training |  | buspirate.com |
| flashrom serprog (Pico / CH341A) | Dump your own SPI flash | USB / SPI | ~$5–10 | Bay · training | Owned devices only | flashrom.org |
| Great Scott Gadgets Cynthion | USB protocol analyzer + HID test harness | USB HS | ~$150 ? | Dock · LAB | Supervised | greatscottgadgets.com |
| Chameleon Ultra | 13.56 MHz emulator and reader | USB / BLE | ~$40–60 ? | Dock · LAB | Own or blank tags only, never real credentials |  |
| Proxmark3 (RDV4 / Easy) | Full HF/LF research tool | USB | ~$75–300 ? | Dock · LAB | Lab only; own or blank tags |  |
| T5577 / MIFARE blank tags | Writable practice targets | 125 kHz / 13.56 MHz | ~$1 each ? | Dock · LAB | Club-supplied blanks only |  |
| Wiegand interface + club test door | Study a club-owned reader and controller | GPIO | ~$10 ? | Bay · LAB | Club's own test door only, never campus infrastructure |  |
| ChipWhisperer-Nano / Husky + PicoEMP / Faultier | Side-channel and fault-injection teaching | USB | ~$50 / $250+ ? | Dock · LAB | Bench only, supervised, isolated targets | newae.com |

## Field, automotive and industrial

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| TI TCAN3413 / 3414 CAN FD module | CAN FD up to 8 Mbps straight off 3.3 V | S31 CAN TX/RX | T1 $5 | Tool bay (Bay B) · LAB | Replaces TCAN1462 (needs 5 V). Listen-only by default | [ti.com](https://www.ti.com/product/TCAN3413) |
| Microchip MCP2518FD | Second CAN FD bus for gateways | SPI + IRQ | Click $44.71 | Bay · LAB | Spin our own; the Click is expensive | digikey.com |
| M5Stack CANBus Unit U085 (CA-IS3050G) | Isolated CAN | Grove TX/RX | $11.95 | Tool bay (Bay B) | Wrap-a-breakout route; CAN FD not verified | [shop.m5stack.com](https://shop.m5stack.com/products/canbus-unitca-is3050g) |
| NXP TJA1021 LIN module | LIN body-bus sniffing | UART | ? | Tool bay (Bay B) · LAB | Powered from the car's 12 V | nxp.com |
| ST L9637D K-line module | ISO 9141/14230 for older cars and bikes | UART | ? | Tool bay (Bay B) · LAB | Open reference: muki01 K-line reader | [github.com](https://github.com/muki01/OBD2_K-line_Reader) |
| Auto cartridge (CAN FD + LIN + K-line + OBD cable) | One connector for every car bus | Full rail | T2 $12 | Tool bay (Bay B) · LAB | Car side powered by the car, never the badge battery |  |
| Macchina A0 (DEV-17493) | Ready-made ESP32 OBD-II dongle | Wi-Fi / BT | $90.50 | Dock | Buy-versus-build benchmark | [sparkfun.com](https://www.sparkfun.com/macchina-a0-obd-ii-development-module.html) |
| TI THVD1450 RS-485 module | Modbus RTU, DMX512, industrial sensors | UART + DE | T1 $5 | Tool bay (Bay B) | SparkFun SP3485 board is $12.50 for comparison | [sparkfun.com](https://www.sparkfun.com/sparkfun-transceiver-breakout-rs-485.html) |
| DMX512 over RS-485 + 5-pin XLR pigtail | Stage-lighting control | Firmware | pigtail ~$5 ? | App (no hardware) | 3-pin XLR DMX isn't standard |  |
| Adafruit MIDI FeatherWing (4740) | Opto-isolated MIDI in/out | UART | $6.95 ($5.56 @100) | Bay | Re-spin with 3.5 mm TRS jacks | [adafruit.com](https://www.adafruit.com/products/4740) |
| USB-MIDI and USB↔RS-485/CAN bridge | MIDI controller; PC gateway | USB | $0 | App (no hardware) | Firmware only |  |
| Adafruit DS2484 (5976) | 1-Wire master for DS18B20 probes and iButton | Qwiic | ~£7.30 ? | Qwiic pod |  | [digikey.ca](https://www.digikey.ca/en/products/detail/adafruit-industries-llc/5976/24639138) |
| Adafruit ISO1540 (4903) | Isolated I2C so pods can touch grounded gear | Qwiic | ~£6.87 ? | Qwiic pod | Manufacturing's off-the-shelf starter | [digikey.co.uk](https://www.digikey.co.uk/en/products/detail/adafruit-industries-llc/4903/13901492) |
| SparkFun QwiicBus EndPoint (PCA9615) | I2C to remote pods over Cat5 | Qwiic | $14.95 ($12.71 @100) | Qwiic pod |  | [sparkfun.com](https://www.sparkfun.com/sparkfun-qwiicbus-endpoint.html) |
| 5 V level shifter module (TXS0108E / TXB0104) | Safe 5 V I/O | GPIO | T1 $5 | Bay | TXB parts misbehave with pull-ups | ti.com |
| Field I/O module | 4 opto inputs + 2 MOSFET outputs, screw terminals | GPIO | T1 $5 | Tool bay (Bay B) | 30 V max; never mains |  |
| SparkFun Qwiic Single Relay / Adafruit 4409 | Switch loads | Qwiic / GPIO | ~$15 / ~$8 ? | Qwiic pod · LAB | Mains switching only in the lab | sparkfun.com |
| DRV8833 / PCA9685 / TMC2209 | DC motors, 16 servos, quiet steppers | GPIO / I2C / UART | ~$5 / ~$15 / ~$6 ? | Dock | Each needs an external supply | adafruit.com |
| MCP9600 (4101) vs MAX31856 (3263) | Thermocouple reading | Qwiic vs SPI | ~$16 / ~$17.50 ? | Qwiic pod | MCP9600 wins: no chip select needed | adafruit.com |
| 4–20 mA (DFRobot SEN0262 or shunt + ADS1115) | Read industrial transmitters | Analog / I2C | ~$10 ? / ~$4 | Tool bay (Bay B) | Needs a 12–24 V loop supply |  |
| Modbus RTU, OBD-II/UDS, J1939, CAN listen-only | Turns the CAN and RS-485 modules into tools | Firmware | $0 | App (no hardware) | Listen-only is the safe default |  |

## Connectors, displays and input

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| Mill-Max 0906 / 0907 spring pins | Host-side contacts for bays and rail | Spring pin on ENIG pads | $0.62 / $0.40 @500 | Part used on modules | 1M cycles, 2 A. Default contact | mill-max.com |
| Mill-Max 0985 | Lower-force spring pin | Spring pin | ? | Part used on modules | 1M cycles; screws, not magnets, for clamp force | mouser.com |
| Mill-Max 0965 (SMT, ultra-low) | Contacts where depth is tight | SMT spring pin | ? | Part used on modules | Check stroke on the datasheet | digikey.com |
| Harwin P70 | Second-source SMT spring pins | SMT spring pin | ? | Part used on modules | 10k cycles; some part numbers obsolete | harwin.com |
| Mill-Max 821-22 spring strips | Pre-aligned multi-pin strips | Through-hole strip | ~$6 @50 | Part used on modules | No hand-aligning loose pins | futureelectronics.com |
| Adafruit magnetic connectors (5358 / 5359) | Self-aligning dock or charging link | Magnetic spring pins | ~$7 ? | Dock | Polarized 5-pin repels if reversed | adafruit.com |
| Hirose DF40 / Molex SlimStack | Permanent internal board-to-board | 0.4 mm mezzanine | ? | Core board | 30 mating cycles: never member-swappable | hirose.com |
| ~~M.2 card edge (TE 2199230)~~ | Reuse MicroMod boards | 67-pin, 0.5 mm | ? | Rejected | ~60 cycles, 4.2 mm tall | sparkfun.com |
| SAO v2 2×3 header | Community badge add-ons | 2.54 mm | <$1 ? | Dock | Sticks out of the case: dock or adapter only | hackaday.io |
| K&J D41-N52 disc magnets | Holds blank covers and rail caps | — | $0.27 | Part used on modules | Too weak for spring-pin clamp force | kjmagnetics.com |
| Stainless ball plunger (Misumi / McMaster) | Rail detent that won't creep like printed plastic | Press-fit or threaded | ? | Part used on modules | Press-fit suits printed parts | misumi-ec.com |
| Adafruit EYESPI 18-pin FPC | Swap display panels without a respin | SPI + touch IRQ | $1.95 | Core board | Fits one way round | adafruit.com |
| Adafruit 1.47" 320×172 IPS ST7789 (5393) | Wide panel that suits a 55 mm case | SPI | $17.50 ($14 @100) | Core board | Mechanical's display pick | adafruit.com |
| Waveshare 1.69" 240×280 IPS | Bigger panel | SPI | ~$10.78 | Core board | Check outline against 55 mm | waveshare.com |
| Waveshare 1.28" round GC9A01 | Watch-face shells | SPI | ~$12.53 | Core board | Wastes the corners | lcsc.com |
| Sharp Memory LCD LS013B7DH05 (Adafruit 3502) | Always-on, microwatt, sunlight-readable | SPI | ~$25 breakout ? | Core board | No backlight. The 2.7" version has a 28-week lead | adafruit.com |
| Adafruit 1.54" e-ink SSD1681 (4196) | Rear name tag visible with power off | SPI | $24.95 | Dock | Mechanical's first bay module (2U); panel is wider than a 24 mm bay | adafruit.com |
| 1.43" AMOLED 466×466 (CO5300) | Premium v2 display | QSPI | ? | Core board | Bare panel availability not verified | waveshare.com |
| Alps SKRHABE010 5-way switch | Core navigation | GPIO | $3.04 ($2.06 @100) | Core board | 140-week quote at one distributor; DigiKey had stock. Buy early | digikey.com |
| Adafruit I2C rotary encoder (4991) | Scrub knob and volume | Qwiic seesaw | $5.95 / $7.95 | Qwiic pod | Starter pick | adafruit.com |
| Adafruit Mini I2C Gamepad (5743) | Joystick + 6 buttons | Qwiic seesaw | ~$10 ? | Qwiic pod | Low stock | adafruit.com |
| Pimoroni Trackball (PIM447) | Menu pointer | I2C 0x0A/0x0B | ~$18.36 | Qwiic pod | Only reliable up to 250 kHz: own mux segment | pimoroni.com |
| M5Stack CardKB v1.1 | Full QWERTY keyboard | I2C 0x5F, Grove | ~$8–10.50 | Qwiic pod | Grove is 5 V; 3.3 V operation not verified | m5stack.com |
| Solder Party BBQ20KBD | BlackBerry keys + trackpad | Qwiic | ~$30 (2022) | Qwiic pod | Discontinued; open design the club could re-spin | bbkb-community.github.io |
| Adafruit MPR121 (1982) | 12 capacitive touch pads | Qwiic | $7.95 | Qwiic pod | Pads can be copper on a cartridge face | adafruit.com |

## Software and app-only features

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| ST M24C16 / M24C02 ID EEPROM | Identity + manifest on every bay and rail module | ID-bus I2C, WP pin | ~$0.20 ? | Part used on modules | At 0x50 on the module's own mux segment | [tildagon.badge.emfcamp.org](https://tildagon.badge.emfcamp.org/hexpansions/eeprom) |
| espressif/elf_loader 2.1.0 | Load catalog apps from microSD without reflashing | Firmware library | Free | App (no hardware) | Lists the ESP32-S31. Needs a stable C ABI export table | [components.espressif.com](https://components.espressif.com/components/espressif/elf_loader/) |
| Flipper .fap model | App manifest, export list, major-version check | Pattern | Free | App (no hardware) | Copy as-is for the CTRLA app catalog | [developer.flipper.net](https://developer.flipper.net/flipperzero/doxygen/apps_on_sd_card.html) |
| Badge.team Hatchery | Self-hostable badge app store | Web (Docker) | Free | App (no hardware) | MicroPython-centric; a static JSON index may be enough | [github.com](https://github.com/badgeteam/Hatchery) |
| espressif/sensor_hub | One sensor API with runtime-registered drivers | Firmware library | Free | App (no hardware) | Fits pod classes: climate, IMU, light, pressure | [components.espressif.com](https://components.espressif.com/components/espressif/sensor_hub) |
| esp-idf-lib drivers | BME280, SHT4x, SCD4x, MAX1704x, INA219/260/3221, VEML7700, ADS111x, PCA9685… | I2C | Free | App (no hardware) | No INA226 (use espp/ina226) | [github.com](https://github.com/esp-idf-lib/core) |
| RadioLib 7.x | SX1262 and CC1101 drivers | SPI + IRQ | Free | App (no hardware) | Registry says all targets; needs FREERTOS_HZ=1000 | [components.espressif.com](https://components.espressif.com/components/jgromes/radiolib) |
| espressif/usb_device_uac 1.3.2 | Badge as a USB sound card + mic | USB | Free | App (no hardware) | Lists the ESP32-S31 | [components.espressif.com](https://components.espressif.com/components/espressif/usb_device_uac) |
| esp_tinyusb MSC | microSD as a USB drive for music and pcaps | USB | Free | App (no hardware) | Unmount on the badge while exported; S31 + SDMMC not verified | docs.espressif.com |
| ok-home/logic_analyzer | Logic capture to PulseView or a web UI | GPIO | Free | App (no hardware) | ESP32/S3/C3 only today: needs an S31 port | [github.com](https://github.com/ok-home/logic_analyzer) |
| ESP-IDF simple_sniffer | Wi-Fi capture to pcap on SD | Wi-Fi | Free | App (no hardware) · LAB | Passive only | [github.com](https://github.com/espressif/esp-idf/tree/master/examples/network/simple_sniffer) |
| 802.15.4 Wireshark sniffer | Thread and Zigbee frame capture | 802.15.4 | Free | App (no hardware) · LAB | Espressif's Nov 2026 blog does it on Zephyr; needs porting | [developer.espressif.com](https://developer.espressif.com/blog/2026/11/zephyr-ieee802154-wireshark-sniffer/) |
| Single-chip Thread border router | Thread↔Wi-Fi bridge for Matter demos | Wi-Fi + 802.15.4 | Free | App (no hardware) | Demo grade; S31 not verified | [github.com](https://github.com/simon/esp32c6-border-router) |
| espressif/esp-now | Chat, meeting check-in, podium OTA | Wi-Fi | Free | App (no hardware) | Day-one starter feature | [github.com](https://github.com/espressif/esp-now) |
| Meshtastic BLE client | LoRa messages through a stock Meshtastic node | BLE | Free | App (no hardware) | Same app switches to the LoRa rail later | [meshtastic.org](https://meshtastic.org/docs/development/device/client-api/) |
| TOTP authenticator | RFC 6238 one-time codes | — | Free | App (no hardware) | Port Open Authenticator; time from SNTP, GPS or the podium | [open-authenticator.github.io](https://open-authenticator.github.io) |
| Password manager (SecureGen reference) | Encrypted vault typed over USB HID | USB HID | Free | App (no hardware) | Experimental; not for club infrastructure | [github.com](https://github.com/makepkg/securegen) |
| DuckyScript interpreter (C) | Runs keystroke scripts from /payloads | USB HID | Free | App (no hardware) · LAB | Never runs without on-device confirmation and training |  |

## Expansion standards and precedents

| Part / module | What it adds | Interface | ~Price | Fits | Notes | Source |
|---|---|---|---|---|---|---|
| Tildagon hexpansion (EMF 2024) | Badge add-on standard with ID EEPROM and apps stored on the module | 20-pad ENIG edge: I2C, Detect, 4 fast + 5 slow GPIO | ~135 designs | Standard / reference | Copied its behaviour (detect-gated power, ID header, mux per port), not its card edge or app auto-run | [tildagon.badge.emfcamp.org](https://tildagon.badge.emfcamp.org/hexpansions/creating-hexpansions) |
| SAO v1.69bis / v2 | Hacker-badge add-on header | 2×3, 2.54 mm: 3V3, GND, I2C, 2 GPIO | Hundreds ? | Dock | No ID beyond an optional EEPROM; header too tall for the pocket. SAO port on the dock | [hackaday.io](https://hackaday.io/project/52950-shitty-add-ons/log/159806-introducing-the-shitty-add-on-v169bis-standard) |
| mikroBUS / MikroE Click | Industry add-on socket | 2×8, 2.54 mm: SPI, I2C, UART, PWM, INT, AN, RST | ~2,000 boards, $10–50 | Dock | ClickID on newer boards only; Linux driver still not mainline. One socket on the dock opens the whole range | [hackster.io](https://www.hackster.io/news/mikroe-s-click-ecosystem-grows-to-2-000-boards-with-the-launch-of-the-nxp-powered-rtc-27-click-8603023162a4) |
| Qwiic / STEMMA QT | I2C cable standard | 4-pin JST SH 1 mm | ~620 products, $5–25 | Core board | Address probing only. Two ports on the badge | [sparkfun.com](https://sparkfun.com/qwiic) |
| Arduino Modulino | Arduino's Qwiic modules plus an 8-channel hub | Qwiic, 3.3 V | ~14 modules ? | Qwiic pod | Address only | [store.arduino.cc](https://store.arduino.cc/products/modulino-hub) |
| Seeed Grove | Classroom sensor system | 4-pin 2 mm latching, 3.3 or 5 V | 300+ modules | Dock | No ID; watch 5 V parts. Dock socket or cable adapter | [wiki.seeedstudio.com](https://wiki.seeedstudio.com/Grove_System/) |
| M5Stack Units / M5-Bus | Grove-like units | HY2.0-4P ports, 5 V | Large ? | Qwiic pod | Needs a 5 V-safe adapter | [docs.m5stack.com](https://docs.m5stack.com/en/learn/interface/mbus) |
| Digilent Pmod | FPGA and MCU peripheral header | 6 or 12 pin, 2.54 mm | Dozens ? | Dock | For FPGA members, on the dock | [digilent.com](https://digilent.com/reference/pmod/specification) |
| Flipper Zero GPIO | Flipper add-on header | 18 pin, 2.54 mm | Dozens | Dock · LAB | No ID; hot-plug can corrupt SD. Lab adapter only; receive-only rules still apply | [docs.flipper.net](https://docs.flipper.net/gpio-and-modules) |
| Framework expansion cards | Laptop port modules | Each card is a USB-C device | ~12 official + community | Standard / reference | ID for free through USB enumeration. The pattern behind 'fast cartridges carry their own USB-C' | [frame.work](https://frame.work/products/usb-c-expansion-card) |
| ~~SparkFun MicroMod~~ | Swappable processor and function boards | M.2 E-key | Shrinking | Rejected | Several boards retired Oct 2025; optional pins fragment. Avoid | [sparkfun.com](https://www.sparkfun.com/micromod-thing-plus.html) |
| Adafruit Feather / FeatherWing | Board form factor with stacking wings | 16 + 12 pins, 2.54 mm | Large ? | Dock | Feather socket on the dock | learn.adafruit.com |
| Raspberry Pi HAT+ spec | Pi add-on ID standard | Dedicated ID_SD/ID_SC bus, EEPROM at 0x50 | Hundreds ? | Standard / reference | Lesson adopted: the ID bus is separate from everything else | [datasheets.raspberrypi.com](https://datasheets.raspberrypi.com/hat/hat-plus-specification.pdf) |
| BeagleBone cape EEPROM | Part number and revision pick the overlay | I2C EEPROM, 4 slots via straps | — | Standard / reference | Lesson: a missing driver must fail gracefully | [bootlin.com](https://bootlin.com/blog/using-the-u-boot-extension-board-manager-beaglebone-boards-example/) |
| Pimoroni Breakout Garden | Slide-in breakout slots | 5-pin I2C, 7-pin SPI edge slots | Dozens ? | Dock | Address only | [shop.pimoroni.com](https://shop.pimoroni.com/products/breakout-garden-mini-i2c-spi) |
| Project Ara / Greybus | Google's modular phone, cancelled 2016 | UniPro + Greybus manifests | — | Standard / reference | Borrowed the manifest idea. Lessons: no maker incentives, speed, battery and cost penalties | [fortune.com](https://fortune.com/2016/09/03/why-google-canceled-project-ara/) |
| BeagleConnect Freedom | Greybus over sub-GHz 802.15.4 to a BeaglePlay | Wireless | Niche | Standard / reference | Idea for later wireless pods over the S31's 802.15.4 | [docs.beagleboard.org](https://docs.beagleboard.org/latest/boards/beagleplay/demos-and-tutorials/greybus-host.html) |
| Moto Mods (2016–18) | Magnetic phone backpacks | Rear pogo pins + magnets | Dozens | Standard / reference | Lesson: freeze the slot pinout across board revisions | [9to5google.com](https://9to5google.com/2018/09/13/moto-z-keyboard-mod-canceled/) |
| Supercon 2025 Communicator | ESP32-S3 LoRa badge | SX1262 + SMA option, SAO, MicroPython + LVGL | One badge | Standard / reference | Reference design for a LoRa rail cartridge | [hackaday.com](https://hackaday.com/2025/10/23/announcing-the-2025-hackaday-superconference-communicator-badge) |
| MCH2022 badge (Badge.Team) | ESP32 + RP2040 + iCE40 FPGA badge | SAO, Qwiic, Pmod | One badge | Standard / reference | Precedent for several cheap standard ports | [certification.oshwa.org](https://certification.oshwa.org/nl000038.html) |
