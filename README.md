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

```
GPIO13 — AD0 (TCK) Purple
GPIO12 — AD1 (TDI) Blue
GPIO15 — AD2 (TDO) Green
GPIO14 — AD3 (TMS) Yellow
GND — GND
```

## Usage

- `./run` will start OpenOCD. It will start and wait for gdb connection, default port is 3333.
- Start gdb in a command shell window. For example:
```
xtensa-esp32-elf-gdb -ex 'target remote localhost:3333' <path to application.elf>
```

## Example 


```
$ ./run
Open On-Chip Debugger  v0.10.0-esp32-20191114-1083-g97ba3a6b (2020-01-02-00:31)
Licensed under GNU GPL v2
For bug reports, read
	http://openocd.org/doc/doxygen/bugs.html
Info : Configured 2 cores
Info : Listening on port 6666 for tcl connections
Info : Listening on port 4444 for telnet connections
Info : ftdi: if you experience problems at higher adapter clocks, try the command "ftdi_tdo_sample_edge falling"
Info : clock speed 20000 kHz
Info : JTAG tap: esp32.cpu0 tap/device found: 0x120034e5 (mfg: 0x272 (Tensilica), part: 0x2003, ver: 0x1)
Info : JTAG tap: esp32.cpu1 tap/device found: 0x120034e5 (mfg: 0x272 (Tensilica), part: 0x2003, ver: 0x1)
Info : Target halted. CPU0: PC=0x40096B0F 
Info : Target halted. CPU1: PC=0x40120E2E (active)
Info : Listening on port 3333 for gdb connections
Info : accepting 'gdb' connection on tcp/3333
``` 

## References

- https://www.aliexpress.com/item/32814913865.html
- https://esp32.com/viewtopic.php?t=3806
- https://docs.espressif.com/projects/esp-idf/en/latest/api-guides/jtag-debugging/index.html
- https://dzone.com/articles/jtag-debugging-the-esp32-with-ft2232-and-openocd
- https://medium.com/@manuel.bl/low-cost-esp32-in-circuit-debugging-dbbee39e508b
- http://openocd.org/doc-release/html/index.html

