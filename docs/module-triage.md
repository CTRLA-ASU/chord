# Chord: Module Triage

**Draft, Nov 2026.** This sorts every module idea so far by where it should live, how hard it is, and whether it's worth doing. Effort and fit are first guesses. Change them as the club learns, especially after the first test print.

- **Rules behind it:** [module interface](module-interface.md).
- **Individual parts:** [parts catalog](parts-catalog.md).

## How modules combine

What can be attached at the same time, and what limits it:

| Limit | Rule | Effect |
|---|---|---|
| One radio head | Every external transmitter lives on the top, one at a time | Two radios means swapping heads, or one combined head |
| Two bays | Bay A + Bay B, receive-only | Two custom modules at once |
| One tool exit | Only Bay B's end opens onto the bottom wall | Only one module that needs a cable or USB out |
| One CAN controller | The S31 has one | A second CAN bus needs an MCP2518FD on the same module |
| Separate I2C channels | Every bay, the head and each Qwiic port get their own mux channel | Address clashes only happen *within* one port |
| Shared power | 3V3 800 mA total; VBAT 1.2 A peak total | Big loads (NFC field, LoRa transmit) are fine together; the badge refuses a combination that overflows |
| Height | About 2.5 mm of parts in a bay *(est.)* | Patch antennas, tubes and big connectors don't go in bays |

## Worked example: GPS + NFC

**Yes, simple, and both run at once:**

| What | Where | Why |
|---|---|---|
| GPS | **Radio head:** LoRa + GNSS head (u-blox M10 with its patch on the head's back face) | The patch antenna is too tall for a bay (~4 mm) and wants sky view. It's receive-only, so it can share the head with LoRa |
| NFC reader | **Bay A:** a club module with a reader IC and a coil on top, under the plastic lid | The back of the badge is a natural "tap here" surface |
| Bay B | Still free for a sensor or a wired tool | |

**Things to get right on the NFC module:**
- **Power:** the reader can draw 100–250 mA while its field is on (check the datasheet). Run it from VBAT_SW (300 mA) through its own regulator, not 3V3_SW (100 mA).
- **Bus:** the ST25R3916 uses I2C address 0x50 (verify), which is the ID chip's address. Run it in **SPI mode** on pads 7–10. A PN532 (0x24) or PN7160 (0x28) can use I2C.
- **Ferrite sheet:** the coil sits right above the battery, and a foil-wrapped cell detunes it. Put a thin ferrite sheet between the coil and the carrier, as phones do.
- **Policy:** reading club and blank tags needs training. Cloning or emulating is LAB-only, on the dock, never real credentials.
- **Open question:** a reader transmits at 13.56 MHz (§15.225), and [decision #6](../planning/decisions.md) asks whether that makes it head-only. If it does, NFC moves into a head, and GPS becomes a pod (SAM-M10Q, off the shelf) so both still work at once.

**Without designing anything,** a beginner can do GPS + NFC today with two pods: a SAM-M10Q GPS pod and an M5Stack RFID 2 pod (training tier).

## Other combinations

| Want | How | At once? |
|---|---|---|
| GPS + LoRa | LoRa + GNSS head | Yes |
| GPS + LoRa + lightning | LoRa + GNSS head, lightning module in Bay A | Yes |
| LoRa + 5 GHz Wi-Fi scanning | Both are transmitters, so both are head-only | No: swap heads |
| NFC (13.56 MHz) + 125 kHz | One bay module with both readers, or one in each bay | Yes |
| CAN + logic analyzer | Both need the tool exit | No: swap, or put the analyzer on the dock |
| Two CAN buses | S31 CAN + an MCP2518FD on one "auto" tool module | Yes, as one module |
| Thermal camera + anything | MLX90640 pod | Yes |
| Keyboard + GPS + LoRa | Keyboard pod, LoRa + GNSS head | Yes |

## Triage

**Effort:**
- **Low:** buy it, or firmware only.
- **Medium:** a simple 2-layer club board around a known reference design (roughly 20–60 member-hours).
- **High:** RF, precision analog, tricky mechanics or certification (100+ hours).

**Verdict:**
- **Now:** good for semester 0.
- **First builds:** the first club-made modules.
- **Later:** after Rev A.
- **Dock:** desk only.
- **Skip:** not worth it.

### Sensing
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| Temp / humidity / pressure / gas (BME688, SHT45) | Pod | Buy | Low | Now |
| CO₂ (SCD-41, STCC4) | Pod | Buy | Low | Now (library) |
| Particulates / all-in-one (PMSA003I, SEN66) | Dock | Buy; they have fans | Low | Dock |
| Light, UV, colour, spectral | Pod | Buy | Low | Now |
| Distance / depth (VL53L4CD, VL53L5CX) | Pod | Buy | Low | Now |
| IMU / orientation (BNO085) | Pod; on the core later | Buy | Low | Now |
| Thermal camera (MLX90640) | Pod | Buy | Low | Now (library) |
| Heart rate / SpO₂ | Pod (needs a finger on it) | Buy | Low | Now (library) |
| Lightning (AS3935) | Bay | Club board | Medium | **First builds**: good first bay module |
| Geiger counter | Dock, or a pod on a cable | Buy | Low | Dock: the tube doesn't fit |
| Load cell / thermocouple / soil | Pod | Buy | Low | Now |

### Positioning
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| GPS, quick | Pod (SAM-M10Q, antenna built in) | Buy | Low | Now |
| GPS, integrated | LoRa + GNSS head | Head board + patch | Medium–High | Later (after the LoRa head works) |
| RTK (centimetre) | Dock | Buy | Low | Dock |
| UWB ranging | Head | Club board around DWM3001C | High | Later, LAB |

### Radios
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| LoRa / Meshtastic | Standard head | Club head board around Wio-SX1262 | Medium | **First builds**: ships with every badge |
| IR blaster + receiver | Inside the standard head | Two LEDs, a receiver and a MOSFET on the head board | Low | **First builds** (with the LoRa head) |
| AM/FM/SW listener (Si4732) | Head | Club head board, telescopic antenna | Medium | Later |
| Weather radio + alerts (Si4707) | Head | Chip-down | Medium–High | Later, maybe |
| 5 GHz Wi-Fi scanner (ESP32-C5) | Head | Module on a head board | Medium | Later, LAB |
| Sub-GHz, receive-only (CC1101 915) | Head | Certified module on a head board | Medium | Later, LAB |
| ADS-B aircraft receiver | Head | Club board around an open design | High | Later, maybe |
| AIS ships, SDR | Dock | Buy (dAISy, RTL-SDR) | Low | Dock |
| Cellular / satellite | Dock | Buy | Low | Dock: their grants need 20 cm from the body |
| Extra 2.4 GHz radios (nRF24, C6, nRF54) | — | — | — | Skip: they duplicate the S31 |
| Ham 2 m / 70 cm (SA818) | Head | Board + filtering | High | Skip for now (licensed only) |
| FM transmitter | — | — | — | Skip (not legal to hand out) |

### Identity and security
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| Tap-to-phone tag (ST25DV16K, passive) | Core or pod | Buy | Low | Now (check-in) |
| NFC reader | Bay A (or head, per decision #6) | Club board: reader IC + coil + ferrite | Medium | Later |
| 125 kHz reader | Pod (ID-12LA, read-only) or bay | Buy / club board | Low / Medium | Now as a pod |
| Secure element lab (SE050, OPTIGA, TROPIC01) | Bay | Tiny club board | Low–Medium | **First builds**: easy and safe |
| Emulation / cloning (Chameleon, Proxmark) | Dock | Buy | Low | Dock, LAB, club-owned |
| Smartcard (ISO 7816) | Dock | Buy | Low | Dock: the card slot doesn't fit |
| iButton | Pod | Buy | Low | Later |
| Wiegand (club test door) | Tool bay | Club board | Medium | Later, LAB |

### Wired tools (tool bay)
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| RS-485 / DMX / Modbus | Tool bay | Club board (THVD1450) | Low–Medium | **First builds**: cheap, useful |
| 5 V level shifter / Bus Pirate-style | Tool bay | Club board | Low–Medium | **First builds** |
| CAN FD / OBD-II | Tool bay | Club board (TCAN3413) | Medium | Later, LAB, listen-only |
| Logic analyzer (RP2350) | Tool bay | Club board, USB-C + probes | Medium–High | Later |
| Field I/O (opto in, MOSFET out) | Tool bay | Club board | Medium | Later |
| SPI flash reader | Tool bay | Club board | Medium | Later |
| Signal generator (DDS) | Tool bay | Club board | Medium | Later, LAB |
| Oscilloscope front end | Tool bay | Club board, precision analog | High | Skip for now: buy a cheap scope |
| JTAG/SWD probe | Dock | Buy (debugprobe, Tigard) | Low | Dock |
| Fault injection / glitcher | Dock | Buy (ChipWhisperer) | Low | Dock, LAB |

### Power and bench
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| Power meter (INA228) | Pod | Buy | Low | Now |
| Qi / solar / booster | Power cover | Club cover + charger parts | Medium | Later |
| USB-C PD analyzer | Tool bay | Club board | Medium–High | Later, maybe |
| PD bench supply, electronic load | Dock | Buy / club desk board | Medium | Dock |

### Input, display, audio
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| Keyboard, encoder, joystick, trackball, macro keys | Pod | Buy | Low | Now |
| Haptics (DRV2605L) | Pod, then the core at Rev B | Buy | Low | Now |
| E-ink name tag | — | Too wide for a bay; SPI, so not a pod | — | Skip for now |
| MIDI in/out | Tool bay (TRS jack exit) | Club board | Medium | Later |
| Mic array, desk speaker | Dock | Buy | Low | Dock |

### Compute and storage
| Module | Best home | How | Effort | Verdict |
|---|---|---|---|---|
| Camera / vision | Dock (Grove Vision AI as a pod is the pocket option) | Buy | Low | Dock / pod |
| FPGA (iCE40) | Tool bay | Club board (needs a 1.2 V rail) | High | Later, maybe |
| ESP32-P4, Linux boards | Dock | Buy | Low | Dock |
| Ethernet | Dock | Buy | Low | Dock: the RJ45 doesn't fit |

## Suggested build order

| # | What | Why first |
|---|---|---|
| 1 | Proto card (blank bay module) | Teaches the module format; every member's first board |
| 2 | LoRa + IR radio head | Ships with every badge, so it's on the critical path |
| 3 | Lightning sensor (bay) | Simple, fun, proves the bay end to end |
| 4 | Secure-element lab (bay) | Tiny board, safe, teaches security |
| 5 | RS-485 / level shifter (tool bay) | Proves the tool exit |
| 6 | NFC reader (bay or head) | Popular; wait for decision #6 |
| 7 | LoRa + GNSS head | After the LoRa head is solid |
| 8 | Logic analyzer (tool bay) | Most useful bench tool, hardest of the early ones |

## Doesn't fit nicely, or too much effort

- **Patch-antenna GNSS, Geiger tubes, e-ink panels in a bay:** too tall or too wide. Use a head, a pod or the dock.
- **Two transmitters at once:** the head holds one. Swap heads.
- **Two cabled tools at once:** one tool exit. Swap, or combine them on one board.
- **Smartcard slots, RJ45, big screens:** too big. Use the dock.
- **Cellular, satellite, 1 W LoRa:** their grants need 20 cm from the body. Use the dock.
- **Oscilloscope front end, glitcher, FPGA:** a lot of effort for something a cheap bench tool already does. Buy them for the dock instead.
- **Extra 2.4 GHz radios:** the S31 already has Wi-Fi, Bluetooth and 802.15.4.

## Fill in as the club decides
| Module | Champion | Status | Issue / PR |
|---|---|---|---|
| | | | |
