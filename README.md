# Filament Clock

A clock built from six circuit boards joined by card-edge connectors: one base board, four plug-in digit boards and a plug-in colon board. Each digit is outlined in neon pink LED filament, so the numbers seem to float.

Designed by [Just Different Creations](https://justdif.com) in Lufkin, Texas. See it on the [PCB-Only Builds](https://justdif.com/pcb-only-builds/) page.

## How it works

- An **ATtiny84A** reads the time from a **DS3231** real-time clock over I2C (bit-banged on the USI peripheral).
- Each of the four digits is sent as a 7-segment pattern to a chain of shift registers on the digit boards. The leading hour digit is left blank when it is 0.
- A separate output drives the colon.
- Time is shown in 24-hour format. Two buttons add one hour or one minute and save the new time to the DS3231.

## Pinout (ATtiny84A)

| Pin | Function |
| --- | --- |
| PA0 | Shift register latch |
| PA1 | Shift register clock |
| PA2 | Shift register data |
| PA7 | Shift register output enable (driven low) |
| PA4 | I2C SCL (DS3231) |
| PA6 | I2C SDA (DS3231) |
| PB0 | Hour button (adds 1 hour, internal pull-up) |
| PB1 | Minute button (adds 1 minute, internal pull-up) |
| PB2 | Colon |

## Building and flashing

- MPLAB X IDE with the XC8 compiler (built with v2.45)
- Device: ATtiny84A, running at 1 MHz (`F_CPU 1000000UL`)
- Programmer: PICkit 5 (any ISP programmer that MPLAB X supports for the ATtiny84A will do)

Open the `.X` folder in MPLAB X, build, and program the board.

## Credits

`DS3231.c`, `DS3231.h`, `USI_I2C_Master.c` and `USI_I2C_Master.h` come from [Pesc0/Clock](https://github.com/Pesc0/Clock), which is licensed under GPL-3.0.

## License

GPL-3.0. See [LICENSE](LICENSE).
