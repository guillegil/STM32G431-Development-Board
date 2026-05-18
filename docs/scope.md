# STM32G431 Dev Board — Project Scope

**Project:** `stm32g431-devboard`
**Goal:** A learning-focused STM32 development board for KiCad practice and future firmware experimentation.
**Out of:** Commercial product, certification target, or anything that needs to "just work" without iteration.

---

## Goals (what success looks like)

1. Functional STM32G431 dev board that boots, runs firmware, and is debuggable
2. Hand-soldered by user (no PCBA service for v1)
3. Manufactured at JLCPCB, assembled in user's workshop
4. Used as both a learning artifact AND a "brain module" for future projects
5. Documents the user's KiCad and STM32 skills development

---

## In scope (locked feature list)

### Power
- USB-C input (GCT USB4085) with 5.1kΩ CC pull-downs
- Diode-OR power input: USB + external (JST-PH 2-pin) both Schottky-protected
- Dual LDO selector (AP2112K-3.3 + MCP1700-3302E/TT) via 3-pin jumper
- Power LEDs with disable jumpers (red on VBUS, green on +3V3_RAW)
- Current measurement jumper between +3V3_RAW and +3V3

### MCU support
- STM32G431CBT6 (LQFP-48)
- VDD decoupling: 3× 100nF + 1× 4.7µF
- VDDA filter: ferrite bead + 1µF + 10nF
- VREF+ selector jumper (internal +3V3A vs external via 1kΩ)
- VBAT tied to +3V3 (no battery backup)

### Programming & debug
- SWD 5-pin header
- Reset button + 100nF noise cap
- BOOT0 button (PB8) + 10kΩ pull-down
- USB-C handles DFU flashing + USB CDC virtual UART (firmware-level)
- Physical UART header (USART2 on PA2/PA3) as backup debug

### User I/O
- User LED on PA5 (1kΩ current limit)
- User button on PB1 with 10kΩ pull-up
- **3× WS2812B addressable RGB LEDs** on PA0 (TIM2_CH1)
- **74AHCT125 level shifter** (3.3V → 5V) for RGB data line

### Protection
- **USBLC6-2SC6 ESD protection** on USB D+/D− lines

### Connectivity
- **GPIO breakout: Black Pill style** (2× single-row 2.54mm headers, ~40-pin DIP form factor)
- Breadboard-friendly board width

### Documentation on PCB
- Pin labels / silkscreen legends
- Test points on key signals (VDD, GND, +3V3A, key debug points)
- Board name + version on silk
- Polarity markings on diodes, LEDs, electrolytic caps

---

## Explicitly OUT of scope (for v1)

These were considered and **deliberately deferred**:

- ❌ Battery management (TP4056 + DW01A + power path) — separate "Battery Management Board" project
- ❌ Buck/boost converter — LDO is sufficient for USB power; buck-boost adds complexity not needed here
- ❌ External crystal — STM32G4 has internal HSI48 + USB clock recovery, no crystal needed
- ❌ Wireless (BLE/WiFi) — separate nRF5340 project
- ❌ Mounting holes — not selected by user (can add to v2 if needed)
- ❌ Sensors (BME280, IMU, etc.) — out of scope
- ❌ Displays (OLED, LCD) — out of scope
- ❌ Audio codec — out of scope
- ❌ More than 3 RGB LEDs — sufficient for "addressable demo"
- ❌ APA102 (SPI-based RGB) — chose WS2812B for the DMA learning value

---

## v2 candidates (good ideas saved for later)

Captured here so we don't lose them, NOT committed to v1:

- Mounting holes (3.2mm clearance for M3 standoffs)
- USB-PD capable connector + IC (negotiate higher voltage from PD chargers)
- I²C-style "QWIIC" connector for sensor expansion
- Tag-Connect SWD pads (smaller footprint than 5-pin header)
- Battery charging via TP4056 + protection IC
- Crystal footprint (DNP by default) for future precise timing experiments
- 4-layer PCB upgrade for better RF/EMI
- Pin labels on bottom silk too (for when board is flipped)

---

## Status snapshot (update as we progress)

### ✅ Done in schematic
- USB-C power input + diode-OR
- Dual LDO selector + LEDs + jumpers
- Current measurement jumper
- MCU VDD/VSS/VBAT/VDDA decoupling
- VREF+ selector
- USB_DP/USB_DM correctly wired (PA12/PA11)
- SWD header
- Reset button + noise cap
- BOOT0 button + pull-down

### 🔜 Pending schematic (in priority order)
1. User LED (PA5) + 1kΩ resistor
2. User button (PB1) + 10kΩ pull-up
3. USBLC6-2SC6 ESD protection on USB data lines
4. Physical UART header (USART2 / PA2,PA3)
5. RGB LED block: 3× WS2812B + 74AHCT125 + decoupling
6. GPIO breakout headers (Black Pill style, both sides)

### ⏳ PCB layout phase (not started)
- Component placement
- Routing
- Ground pour
- Silkscreen labels & test points
- DRC + 3D check

### ⏳ Fabrication phase (not started)
- Gerbers
- BOM
- JLCPCB order

---

## When new feature ideas arise

**Rule:** if it's not in "In scope" above, default answer is **v2**.

The only exception: a genuine v1 requirement we missed. In that case, the trade-off should be:
- Add the new feature **and** remove something from v1, OR
- Add to v1 only if it's <30 min of work and doesn't change architecture

If the answer is "but it would be cool" → v2.

---

*Last updated: Session creating addressable RGB LED + GPIO breakout decisions*
