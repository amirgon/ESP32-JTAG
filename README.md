# ESP32 FT232H JTAG Debugging on Linux

## Prerequisites

- ESP-IDF installed.
- [ESP32 OpenOCD dependencies](https://docs.espressif.com/projects/esp-idf/en/latest/api-guides/jtag-debugging/building-openocd-linux.html#install-dependencies)
- [Build ESP32 OpenOCD](https://docs.espressif.com/projects/esp-idf/en/latest/api-guides/jtag-debugging/building-openocd-linux.html#build-openocd). It's included as a submodule of this repo.
- ELF file of the compiled firmware such as `application.elf`.

## FTDI Board

I'm using a 7$ [CJMCU FT232H](https://www.aliexpress.com/item/32814913865.html) from AliExpress.

![Image of CJMCU FT232H](https://ae01.alicdn.com/kf/HTB1u03laYwTMeJjSszfq6xbtFXaA.jpg)

## FTDI Hardware connection

GPIO13 — AD0 (TCK) Purple
GPIO12 — AD1 (TDI) Blue
GPIO15 — AD2 (TDO) Green
GPIO14 — AD3 (TMS) Yellow
GND — GND

## Usage

- `./run` will start OpenOCD. It will start and wait for gdb connection, default port is 3333.
- Start gdb in a new window:
```
xtensa-esp32-elf-gdb -ex 'target remote localhost:3333' <path to application.elf>
```

 
