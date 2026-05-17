# STM32G431 Development Board

KiCad 10 design files for a small development board based on the STMicroelectronics
STM32G431CBT6 microcontroller (Cortex-M4F, 170 MHz, 128 KB flash, USB).

This is a personal learning project — my first custom-designed PCB, built as
preparation for a more complex nRF5340-based wireless keyboard development board.

## Features

- STM32G431CBT6 in LQFP-48 package (hand-solderable)
- USB-C connector for power and native USB device communication
- 3.3 V LDO regulator
- SWD programming header
- UART debug header
- User LED + user button
- Reset button + boot-mode jumper
- GPIO breakout headers for experimentation

## Project goals

- Learn KiCad 10 schematic and PCB design workflow
- Learn home reflow soldering (hot plate + hot air)
- Build a base for future Zephyr RTOS experimentation
- Prepare skills for a larger custom-keyboard project

## Status

🟡 In design — schematic in progress

## Tools used

- KiCad 10.x
- Zephyr RTOS / nRF Connect SDK (firmware, future)
- JLCPCB (PCB fabrication, planned)

## License

See [LICENSE](LICENSE). This project is open source under the MIT License.
