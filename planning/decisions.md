# Decision log

Keep this current. When something is decided, move it to **Decided** with the date and a link to the issue or PR where it was discussed.

## Open

| # | Decision | Options on the table | Needed by | Owner | Status |
|---|---|---|---|---|---|
| 1 | ESP32-S31 go/no-go | S31 / ESP32-S3 dev boards as a fallback | Mid-Dec 2026 | | Open |
| 2 | Display | 1.3" 128×64 mono OLED / 1.47" 320×172 colour IPS | Before the Rev A schematic (week 3) | | Open |
| 3 | Rear pack height | ~6.9 mm with 2.5 mm parts / 6.0 mm with ~1.6 mm parts | After the first test print | | Open |
| 4 | LoRa head ships to every member | Yes, region-locked / earned upgrade after training | Before Rev B | | Open (about +$10–14 per badge) |
| 5 | Licenses | CERN-OHL-W-2.0 (hardware), Apache-2.0 (firmware), CC-BY-SA-4.0 (docs), as proposed | Before the first hardware files | | Open |
| 6 | NFC readers: head or bay? | They transmit at 13.56 MHz, so possibly head-only | Before NFC module work | | Open |
| 7 | Deposit amount | About $40, refundable, with hardship waivers | Summer 2027 | | Open |
| 8 | Spring-pin part | Mill-Max 0906/0907 / Harwin / generic | After samples | | Open |
| 9 | Head release | Detent only / button | After a test print | | Open |
| 10 | Tool-exit connectors | Which parts fit under ~3 mm | Before tool modules | | Open |
| 11 | I/O expander + Qwiic 2 switch parts | | Rev A schematic | | Open |
| 12 | Vendor IDs for member modules | e.g. one per member or team, assigned by PR | Before the first member module | | Open |
| 13 | University sign-off | IT, card office, faculty advisor | Before any transmit, RFID or keystroke feature ships | | Open |
| 14 | Confirm I2C addresses and module sizes | From datasheets (several are from memory) | Rev A schematic | | Open |

## Decided

| Date | Decision | Where |
|---|---|---|
| Nov 2026 | Use the certified S31 module, not the bare chip | [design-decisions](../docs/design-decisions.md) |
| Nov 2026 | No stacked boards; one rear pack with two bays | [expansion-system](../docs/expansion-system.md) |
| Nov 2026 | Every external radio lives in the radio head, one active at a time | [expansion-system](../docs/expansion-system.md) |
| Nov 2026 | FIDO2 is teaching-only; real logins use certified keys | [design-decisions](../docs/design-decisions.md) |
| Nov 2026 | Sub-GHz (CC1101) ships receive-only | [design-decisions](../docs/design-decisions.md) |
| | | |
