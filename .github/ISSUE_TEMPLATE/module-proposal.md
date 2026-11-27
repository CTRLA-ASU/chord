---
name: Module proposal
about: Propose a bay module, radio head, pod adapter or power cover before designing it
title: "[Module] "
labels: module
---

## What it does
<!-- One or two sentences. What can a member do with it? -->

## Where it goes
<!-- Work through "Where does my module go?" in docs/module-interface.md §12 and tick one. -->
- [ ] Radio head (it transmits RF)
- [ ] Tool bay, Bay B (cable or USB out of the badge)
- [ ] Qwiic pod (off-the-shelf I2C board)
- [ ] Bay A or B
- [ ] Power cover
- [ ] Dock

## Parts and rough cost
| Part | Purpose | Price (est.) |
|---|---|---|
| | | |

## Fit check
| Item | Value | Limit |
|---|---|---|
| Board size | | Bay: 24 × 64 mm · Head: ~50 × 14 × 12 mm inside |
| Tallest part | | Bay: ~2.5 mm · Tool exit: 3.0 mm |
| Peak current on 3V3 | | Bay 100 mA · Head 300 mA |
| Peak current on VBAT | | Bay 300 mA · Head 1 A peak |
| Pads/pins used | | Bay: I2C, SPI (1 CS), IRQ, IO |
| I2C addresses | | Not 0x50; no clashes |

## Radio and safety
- Does it transmit? If so, which module and FCC ID:
- Does it need LAB (transmit, emulate, inject, glitch)?

## Software
- Driver name (e.g. `ctrla,as3935`):
- Apps it unlocks:

## Who's building it
- Designer(s):
- Reviewer(s):
- Target date:
