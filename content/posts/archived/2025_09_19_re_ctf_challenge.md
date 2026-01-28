+++
date = '2025-09-19T10:05:15+02:00'
draft = true
title = '2025_09_19_re_ctf_challenge'
+++

# asd

Examinations:

Launch openocd server, set the debugger and then the target, files are available at ```/usr/share/openocd/scripts/```. (stlink-v2-1.cfg is deprecated)

```bash
└┌(~)┌¨˙openocd -f interface/stlink.cfg -f target/stm32f1x.cfg
Open On-Chip Debugger 0.12.0
Licensed under GNU GPL v2
For bug reports, read
	http://openocd.org/doc/doxygen/bugs.html
Info : auto-selecting first available session transport "hla_swd". To override use 'transport select <transport>'.
Info : The selected transport took over low-level target control. The results might differ compared to plain JTAG/SWD
Info : Listening on port 6666 for tcl connections
Info : Listening on port 4444 for telnet connections
Info : clock speed 1000 kHz
Info : STLINK V2J40M27 (API v2) VID:PID 0483:374B
Info : Target voltage: 3.250952
Info : [stm32f1x.cpu] Cortex-M3 r1p1 processor detected
Info : [stm32f1x.cpu] target has 6 breakpoints, 4 watchpoints
Info : starting gdb server for stm32f1x.cpu on 3333
Info : Listening on port 3333 for gdb connections
```

Connect with a gdb session and dump the firmware on it (0x20000 is 128kB):

```bash
arm-none-eabi-gdb
```

```bash
(gdb) target extended-remote :3333
(gdb) monitor reset halt
(gdb) monitor dump_image dump.bin 0x080000000 0x20000
```

```bash
dumped 131072 bytes in 1.980690s (64.624 KiB/s)
```

ghidra debug
- set memory map for
  - flash
  - flash mirror
  - sram
  - load cmsis svd file (couldnt get the correct one yet)



Theres the possibility to write your own startup code and ill od that for learning purposes.

In the RM08000 manual the vector table setup is the following, see Table 63. Vector table for other STM32F10xxx devices.

there are 13 system interrupts and 60 IRQs
 - the first is reserved for the MSP master stack pointer 0x0000 0000, the next is the Reset handler @ 0x0000 0004

# References

![alt text](image.png)

STM32F103RB Nucleo 64 board:
 - https://www.keil.arm.com/boards/stmicroelectronics-nucleo-f103rb-revc-733985f/documentation/
 - https://www.st.com/resource/en/data_brief/nucleo-f103rb.pdf
 - https://www.st.com/resource/en/user_manual/dm00105823.pdf
 - https://www.st.com/resource/en/datasheet/stm32f103rb.pdf

Cortex M3 TRM:
 - https://www.keil.com/dd/docs/datashts/arm/cortex_m3/r1p1/ddi0337e_cortex_m3_r1p1_trm.pdf

stm32f103xx RM0008 Reference manual:
 - https://www.st.com/resource/en/reference_manual/rm0008-stm32f101xx-stm32f102xx-stm32f103xx-stm32f105xx-and-stm32f107xx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf

vector table video:
 - https://www.youtube.com/watch?v=2Hm8eEHsgls