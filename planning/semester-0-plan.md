# Semester 0 plan (Spring 2027)

The goal by the end of the semester: a working Rev A on the bench, firmware running on it, the module interface tested with printed parts, and a Rev B plan for the summer. Fill in owners as people sign up. Shift weeks to match the real academic calendar.

## Before the semester (Dec 2026 – Jan 2027)
- [ ] **ESP32-S31 go/no-go (mid-Dec).** Go only if all three hold; otherwise start on ESP32-S3 dev boards. Owner: ____
  - [ ] the module's FCC grant is published
  - [ ] 100+ modules are quoted
  - [ ] a dev board runs A2DP, high-speed USB and SDMMC on ESP-IDF 6.1.x
- [ ] Order 10+ dev boards and breakouts: display options, ES8388 board, microSD, Wio-SX1262, a few Qwiic pods. Owner: ____
- [ ] Fill in [team.md](team.md): five subsystem owners plus understudies.
- [ ] Start conversations with the faculty advisor, university IT and the card office (needed before any transmit, RFID or keystroke feature). Owner: ____
- [ ] Decide licenses (see [decisions.md](decisions.md)). Owner: ____

## Weeks 1–4: foundations
| Track | Tasks | Owner |
|---|---|---|
| Firmware | Set up ESP-IDF 6.1.x for everyone; display, microSD and codec working on a dev board; ESP-NOW chat demo | |
| Hardware | Split the Rev A schematic into blocks and assign them; **decide the display by week 3** | |
| Mechanical | First test print: carrier, blank bay module, head shell. Measure the real height budget | |
| Program | Onboarding night, starter pods, skill tree kickoff | |

## Weeks 5–8: Rev A design
| Track | Tasks | Owner |
|---|---|---|
| Hardware | Schematic review (week 6), layout (weeks 7–8), two sign-offs, DFM check | |
| Firmware | LoRa over SPI (RadioLib); ID-chip reader + manifest parser on a proto card; USB drive + USB sound card | |
| Mechanical | Second print; spring-pin samples; pick the head detent | |
| Modules | New KiCad members design the proto card and one bay module (e.g. lightning sensor) | |

## Week 9: order Rev A
- [ ] 5–10 assembled boards ordered. Owner: ____
- [ ] Proto cards and the first module board ordered with it.

## Weeks 10–11: buffer (midterms)
Firmware and module design continue; nothing on the critical path.

## Weeks 11–14: Rev A bring-up
- [ ] Follow [rev-a-bring-up.md](rev-a-bring-up.md) and record results.
- [ ] Measure runtime per mode with the fuel gauge.
- [ ] Write the Rev B fix list.

## Weeks 15–16: plan the summer
- [ ] Rev B plan: fixes, shrink to 51 × 91 mm, test fixture.
- [ ] Candidate freeze of the module interface (v1.0) for Rev B.
- [ ] Deposit amount and ordering plan for Fall 2027.
- [ ] Summer owners and meeting schedule.

## Later milestones
| When | Milestone | Done? |
|---|---|---|
| Mid-July 2027 | Rev B design freeze | |
| ~Week −4 before fall | Production order placed | |
| Fall 2027 | Every member gets a Chord with the LoRa head | |
| 2028 | Rear pack, more heads, monthly KiCad sprints | |
