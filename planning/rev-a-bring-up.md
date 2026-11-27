# Rev A bring-up checklist

**Work through this one board at a time, in order.** Stop at the first failure, write it down, and fix it before going on.

**Safety:**
- Use a current-limited bench supply until step 4 passes.
- Keep the LiPo disconnected until step 6.
- Never leave a charging board unattended.

## Steps
1. **Look first.** Check under magnification for solder bridges, part orientation (ICs, diodes, battery connector polarity) and missing parts.
2. **No-power checks.** Measure resistance from each rail to GND. Nothing should read near 0 Ω.
3. **First power.** Use a bench supply on VBAT at 3.7 V with a 100 mA limit. Watch the current, then close each rail jumper one at a time.
4. **Rails.** Measure 3V3 and the analog audio rail; record voltage and ripple.
5. **USB-C.** Plug in 5 V and confirm the TPS2121 picks USB and the charger LED and status behave.
6. **Battery.** Connect a protected cell with the polarity checked. Confirm charging current and the hard-off button, and read the MAX17055.
7. **S31.** Confirm it enumerates over USB-Serial-JTAG, flash a test build, and read the chip ID.
8. **I2C scans.** Every bus should show exactly the expected addresses: I2C0 (codec, gauge, RTC, expander), LP-I2C (ATECC608B), and the mux at 0x70 with each channel stepped through.
9. **One subsystem at a time:**
   - display
   - microSD
   - buttons and 5-way switch
   - RGB LED
   - codec: headphone and speaker, plus an FFT noise check on the headphone output
   - microphone
10. **Ports:**
    - Proto card in each bay: ID read, power enable, eFuse trip test with a deliberate overload, and the lid interlock.
    - LoRa head prototype: DET, SPI, a LoRa packet sent and received.
    - Qwiic: both ports, plus port 2 in UART mode.
11. **Radios.** Wi-Fi and Bluetooth connect, and the signal strength looks sane next to a dev board.
12. **Power profile.** Measure current per mode (idle, Bluetooth audio with the screen off, Wi-Fi scan with the screen on, LoRa transmit) and work out runtime.
13. **Heat.** Check for hot spots after 30 minutes of the heaviest mode.

## Results

| Board # | Step | Expected | Measured | Pass? | Notes / fix needed | Who | Date |
|---|---|---|---|---|---|---|---|
| | 4 · 3V3 rail | 3.30 V ± 3% | | | | | |
| | 4 · Audio rail ripple | < 50 µV in the audio band | | | | | |
| | 6 · Charge current | (set value) | | | | | |
| | 6 · Off-state drain | < 30 µA | | | | | |
| | 12 · BT audio, screen off | (mA) → hours | | | | | |
| | 12 · Wi-Fi scan, screen on | (mA) → hours | | | | | |
| | | | | | | | |

## Rev B fix list
| # | Problem | Fix | Owner | Done |
|---|---|---|---|---|
| | | | | |
