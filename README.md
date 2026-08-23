# Motorola 68030 SBC
Note/warning: This is WIP, not yet tested on real HW.

## Intro
Ah, yes, yet another project.  
Idea is to learn something and have fun while doing it. I never designed computer from the ground up.  
M68030 is chosen because it contains MMU, so maybe one day it will run NetBSD or homemade OS.  
Also, this [Reddit post](https://www.reddit.com/r/m68k/comments/n1wkd5/any_68k_designs_with_external_mmus/) explains it nicely:  
> The 68K series is at a point where it is old/slow enough that you can work with the real hardware and understand everything that is going on electronically, but is new/fast enough that it run some modern software (very slowly).  

I am experienced in MCU world (from 8-bit AVRs long time ago to multi core RISC-V), but this is my first CPU.  
It is interesting to see that, in comparison to MCUs, this thing doesn't have much. No RAM, no EEPROM, no systick, no UARTs, no SPI, no I2C, not even GPIO, nothing.  
And that is fun part!  
This will be built as multiple PCBs, so it can be easy patched and respin if needed. I prefer SMD, so that will be used when available. Address decoder and other stuff will be implemented in pure logic (74000 series), no CPLD for now. Modularity will also help with replacing discrete logic with CPLD if/when needed.  
Design not tested on breadboard nor simulator, I am doing this on paper first and then on PCB. Parts will be in TSSOP packaging if possible  
Tricky part will be availability of 30+ old (legit) parts and verifying design without knowing if fault is because of SW, HW design error or counterfeit part.  
This won't be cheap (money and time wise). But it will be fun!  

## Plan
- investigation, part hunting, planning HW
- draw PCBs for CPU, SRAM, flash, UART and then order them simultaneously
- find a way to flash inital ROM from PC
- while waiting for parts, try to build and run some sort of ROM monitor in QEMU
- HW verification
	- check CLK signal
	- check reset circuit
	- free running
		- tie all data lines to 0
		- put few LEDs on upper address pins
		- slow down the clock?
		- 68k will run through address space
		- watch LED blink
	- run something from ROM
- verify that CPU, address & data bus, SRAMs, ROM, discrete logic, and misc parts are working
- replace discrete logic with CPLD
- implement DRAM
- implement ATA
- add network
- run NetBSD on it

## [Examples - others](./docs/examples-others.md)
Examples of M68k homebrew projects, made by others, used for learning and motivation purposes

## [Selection of HW parts](./docs/hw-parts.md)
Possible list of parts which can be used

## [my HW](./hw/pcb/)
- stack of multiple 100x100 mm PCBs
- 2 layer PCB
- make it aesthetically pleasing:
	- put ICs at top
	- put passives at bottom
	- hide IC markings under ICs
- board interconnects: male-female pin headers with:
	- 2x32 addr
	- 2x32 data
	- power
	- misc/ctrl MC68030 signals:
		- 27 signals
		- 9 optional or NC signals
- PCBs:
	- CPU + clk + reset button
		- few LEDs which will help with free running
	- SRAMs + ROM
		- with some way of programming ROM without removing (desoldering) it
	- address decoders
		- discrete logic first
		- CPLD later
	- UARTs + USB UARTs + USB hub + PWR in

## [SW](./docs/sw.md)
