# Chord: Design Decisions

**Draft, 26 Nov 2026.** This summarizes the design review of the original spec ("CTRLA Continuous Club Project: The Modular CTRLA Token & Multi-Tool Ecosystem"). Each area was reviewed separately: architecture, silicon, power and PCB, audio, RF and regulatory, mechanical, firmware, security and legal, manufacturing and cost, and the club program. Contested points were then settled together.

- **Expansion design:** radio head, rear pack, bays and pods are covered in [expansion-system.md](expansion-system.md).
- **Candidate parts:** see [parts-catalog.md](parts-catalog.md).
- **Prices are estimates.** None are live quotes.

## The short version

- The idea holds up. The original spec tried to do too much at once, and its 16-week plan was about three times too short.
- **Build a small, well-tested core first.** Expand it through one module interface, and spread the work over several semesters, starting with dev-board prototypes.

## 1. Core hardware

| Area | Decision | Why |
|---|---|---|
| Processor | **ESP32-S31-WROOM-3** module (16 MB flash + 16 MB PSRAM in package), not the bare chip | Pre-certified radio, and no RF, PSRAM or high-speed USB layout for students. The spec's 32 MB PSRAM isn't available |
| SDK | ESP-IDF pinned to **6.1.x** | S31 support is still marked preview |
| Charger | **BQ24074** only | The TP4056 can't run the device while charging |
| Regulator | Buck-boost (TPS63802 or TPS63020), enabled by a push-button controller with a long-press hard-off | Off-state drain under 30 µA |
| Fuel gauge | **MAX17055** | Measures real current per app, so runtime can be published per mode |
| Battery | **604065**, 2000 mAh, with a protection board, NTC and UN38.3 certification. 1 mm swell gap. Students never solder cell tabs | A 503759 is only about 1300 mAh |
| Audio | **ES8388** codec + **NS4150B** speaker amp, on a dedicated low-noise LDO | The WM8960 is obsolete, and the PCM5102A has no headphone amp |
| Microphone | **TDK T5838** PDM, with wake-on-sound | The ICS-43434 and INMP441 are end-of-life |
| Storage | microSD on 4-bit **SDMMC** | Keeps it off the shared SPI bus |
| Display | On its own SPI bus. **Still open:** a 1.3" 128×64 mono OLED (SH1106/SSD1309) or a 1.47" 320×172 colour IPS (ST7789) | The OLED saves backlight power and roughly $10; the IPS is richer. Decide before Rev A |
| CAN | **TCAN3413** (3.3 V) | The TCAN1462 and MCP2562FD need 5 V |
| Secure element | **ATECC608B** on a private I2C bus | The 608A isn't for new designs |
| GNSS | **u-blox M10** (MAX-M10S / SAM-M10Q), in a radio head | Replaces the NEO-M8N. Patch antennas are too tall for a bay |
| Navigation | Alps **SKRHABE010** 5-way switch | One distributor quoted 140 weeks, so buy early |
| Board | 4-layer, all SMT on the top side, test points on every rail. Rev A for bring-up, Rev B for final size | The flat bottom faces the battery, and single-side assembly is cheaper |

**Runtime** will be published per mode rather than as one headline number. Rough estimates for 2000 mAh:

| Mode | Runtime |
|---|---|
| Bluetooth audio, screen off | ~15 h |
| Wi-Fi sniffing with the screen on | 7–8 h |
| With a power-hungry module running | 5 h or less |

## 2. Radio and RF rules

- **Certified modules only.** Every transmitter is a module with its own FCC ID; no chip-down radios.
- **One transmitter, one place.** External transmitters live only in the radio head, and only one is active at a time.
- **No nRF24 walkie-talkie.** Voice runs over ESP-NOW first, then LoRa (Codec2) later. Voice and Bluetooth audio can't run at the same time.
- **Sub-GHz is receive-only.** The CC1101 module ships receive-only. Transmit is taught in a shielded box or into a cable, and licensed hams build their own 433 MHz gear.
- **Wi-Fi capture is passive only.** No deauth, no jamming, and no keeping payload content.
- **Antennas and labels:**
  - Only antennas listed in each module's grant, on RP-SMA connectors.
  - Each unit is labelled "Contains FCC ID…" with a Part 15 statement.
- **Compliance review:** these rules are the design review's reading of FCC Part 15, not legal advice. Route the plan through university compliance.

## 3. Security and responsible use

- **FIDO2 is a teaching app only.** It is never registered for real club, GitHub or server logins, and real accounts use certified keys. A reflashable device that runs scripts can't be a trustworthy authenticator.
- **Meeting check-in can't be faked.** Each badge signs a fresh challenge with its ATECC608B, so a copied beacon can't be replayed.
- **RFID/NFC: club-issued and blank tags only.** Never clone or emulate a campus ID, payment card, door fob or any credential you aren't authorized to hold.
- **Keystroke payloads ask first.** They never run without confirmation on the device and completed training.
- **LAB tier** covers emulation, transmit, fault injection and keystroke injection:
  - LAB hardware is club-owned and loan-only.
  - PCB credits for LAB designs need a design review.
  - Members sign the acceptable-use policy and complete training.
  - The firmware LAB flag is a guardrail, not enforcement.
- **Sign-off first.** Get written approval from university IT, the card office and the faculty advisor before distributing transmit, RFID or keystroke features.

## 4. Firmware

- **A thin platform on ESP-IDF:** LVGL UI, TinyUSB, esp-audio-codec and RadioLib.
  - Borrow from Bruce, Marauder and pico-fido after a license audit, since several are GPL.
  - Core 0 runs the radios. Core 1 runs audio, the UI and scripts, and nothing may block audio.
- **Partitions:** factory recovery, ota_0, ota_1, NVS, LittleFS, and an encrypted partition for keys.
- **Member units stay reflashable,** so no secure boot is burned on them.
  - Over-the-air images from the club's podium unit are signed at the app level.
  - Unsigned builds show a "dev build" banner.
- **Scripting:**
  - A C keystroke-script interpreter comes first.
  - MicroPython is a stretch goal from about week 8, because there's no official S31 port yet.
  - Catalog apps load from microSD through `elf_loader`.
- **Module discovery and manifests:** see [expansion-system.md §11](expansion-system.md#11-firmware-behaviour).
- **CI:**
  - ESP-IDF CI builds, host-side tests and a binary-size budget
  - a manifest validator
  - one hardware-in-the-loop runner (pytest-embedded)
- **Day-one features:**
  - UI shell
  - wired MP3/FLAC
  - ESP-NOW check-in
  - Meshtastic messaging
  - the badge as a USB drive and a USB sound card

  Bluetooth A2DP comes next. LE Audio stays experimental.

## 5. Timeline

| When | What |
|---|---|
| **Mid-Dec 2026** | Go/no-go on the S31: a published FCC grant, 100+ modules quoted, and a dev board showing A2DP, high-speed USB and SDMMC working on ESP-IDF 6.1.x. Fallback: ESP32-S3 dev boards for spring |
| **Spring 2027** (semester 0) | Work on dev boards. Beginners build apps from week 2. Advanced members do the Rev A schematic and layout with reviews, order around week 9, and bring up in weeks 11–14 |
| **Mar 2027** | Check module stock for the production run (500+ at the assembler, or buy and consign) |
| **Summer 2027** | Rev B. Design freeze about six weeks before the fall build (mid-July); production order by week −4 |
| **Fall 2027** | Every member gets a Chord: core + LoRa radio head |
| **2028** | Rear pack and more heads, then monthly KiCad sprints for member-designed modules |

## 6. Cost and manufacturing

**Cost (estimates, not live quotes)**
- **Per badge:** about $40–48 at 200 units, plus about $10–12 for the standard LoRa head.
- **Prototypes:** budget about $1.5–2k for board revisions.

**Funding**
- A refundable hardware deposit of about $40, separate from dues, with hardship waivers.
- The order quantity equals the number of paid deposits.
- Sponsor credits cover boards and assembly. The club or cash sponsors cover the rest.

**Building them**
- **Assembly:** turnkey, with all SMT parts on the top side. Members fit the battery and through-hole parts at a build night, checking connector polarity on every lot.
- **Batteries:** order about 60 days ahead, because hazmat shipping adds 2–4 weeks. Test every cell on arrival for voltage, protection and polarity.
- **Testing:** a pogo-pin test fixture (about $150) runs a test of under 60 seconds. Expect 97–98% of boards to pass first time.
- **Cases:** about 3.5 printer-hours each. Parts that hold contacts (carrier, head shells) are printed centrally or ordered in MJF nylon; members print only cosmetic parts, after a club clearance test print.

## 7. Team and governance

- **Ownership:** five subsystem owners (power, RF/MCU, audio, mechanical, firmware), each with a named understudy.
- **Reviews:** interface changes go through RFCs. No board is ordered without two reviewer sign-offs on schematic, layout and DFM.
- **GitHub org:** at least two faculty or alumni owners, branch protection, CODEOWNERS per subsystem, DCO sign-off, and docs as code.
- **Licenses (proposed):**
  - CERN-OHL-W-2.0 for hardware
  - Apache-2.0 for firmware
  - CC-BY-SA-4.0 for docs and CAD

  GPL code such as Meshtastic stays separate. None of these are adopted yet.
- **Beginners:**
  - starter pods: pick two, $20 cap; the default pair is the VL53L4CD distance sensor + LTR390 UV/light sensor
  - a skill tree with Sense, Make and Share branches
  - a lending library of about $450–550 (thermal camera, air-quality station, CO₂, Geiger counter and more)
  - Pod of the Month, and a demo day

## 8. What the review corrected in the original spec

| Spec said | Correction |
|---|---|
| Up to 32 MB PSRAM | 16 MB is the in-package maximum on the module |
| TP4056 charger | It has no power path, so the BQ24074 only |
| PCM5102A "+ headphone amp" | It's line-out only, so use the ES8388 + NS4150B. The WM8960 is obsolete |
| INMP441 microphone | End-of-life, so use the T5838 |
| SN65HVD230 for CAN FD | Not CAN FD rated, so use the TCAN3413 |
| ATECC608A, NEO-M8N | Use the ATECC608B and u-blox M10 |
| nRF24 voice walkie-talkie | Dropped in favour of ESP-NOW, then LoRa |
| CC1101 capture/replay | Ships receive-only, because replay transmit can't be certified |
| 2–4 stacked rear boards | 25–49 mm thick. Replaced by a two-bay rear pack (about 21 mm) |
| Display on shared I2C | Its own SPI bus |
| microSD on the shared SPI bus | 4-bit SDMMC |
| Module ID EEPROMs at 0x50–0x57 on one bus | One ID chip per module, each on its own mux channel |
| 12–18 h runtime | True only for Bluetooth audio with the screen off; runtime is published per mode |
| Motherboard in weeks 1–4 | Dev boards first; every member gets a badge in Fall 2027 |
| FIDO2 key for club and GitHub logins | Teaching only; real logins use certified keys |
| ESP-NOW broadcast check-in | Signed challenge, so it can't be spoofed |

## 9. Open decisions

- **Display:** mono OLED or colour IPS.
- **Expansion v0.2 changes:** the radio-first changes still need review ([list](expansion-system.md#13-changes-from-the-panels-cmi-v01)).
- **NFC readers** transmit at 13.56 MHz. Do they belong in a head or a bay?
- **FCC:** the S31 module's grant (not published yet), and the LoRa module's antenna list and handheld conditions.
- **Budget:** the standard LoRa head against the $40 deposit.
