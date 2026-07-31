# Motorola 68030 SBC

Ah, yes, yet another project.
Idea is to learn something and have fun while doing it. I never designed computer from the ground up.
M68030 is chosen because it contains MMU, so maybe one day it will run NetBSD or homemade OS.
I am experienced in MCU world (from 8-bit AVRs long time ago to multi core RISC-V), but this is my first CPU.
It is interesting to see that, in comparison to MCUs this thing dont have much. No systick, no UARTs, no SPI, no I2C, not even GPIO, nothing.
And that is fun part!
This will be built as multiple PCBs, so it can be easy patched and respin if needed. I prefer SMD, so that will be used in available. Address decoder and other stuff will be implemented in pure logic (74000 series), no CPLD for now. Modularity will also help with replacing discrete logic with CPLD if/when needed.
Design not tested on breadboard nor simulator, I am doing this on paper first and then on PCB. Parts will be in TSSOP packaging if possible
Tricky part will be availability of 30+ old (legit) parts and verifying desing without knowing if fault is because of SW, HW design error or counterfeit part.


## Insipiration
[Mackerel-68k](https://github.com/crmaykish/mackerel-68k)
- multiple projects: 68010, 68020, 68030
- uses DRAM
- uses CPLDs
- boots Linux

[Computie K30v2](https://github.com/transistorfet/computie/)
- mostly SMD
- 2 MB SRAM
- no CPLD - 74HC logic used
- 512 kB of flash (for ROM only?)
- CF card
- SRAM, flash and CF directly connected to address and data lines
- custom DIY OS: Gloworm
- 12 MHz clock (for 12 MHz varinat of the chip)

[Computie K30p](https://github.com/transistorfet/retroverse/)
- uses CPLD ATF1508AS
- 4MB SRAM
- maybe later 128 MB DRAM

[Simple 010](https://github.com/harrowm/Simple010)
- based on Rosco
- 68010
- CPLD ATF1508
	- HW SPI for SD card
	- (single) UART, compatible with MC68681
- 1 MB SRAM
- 4 MB flash
- 4 layer PCB (as others)

[68K-nano](https://github.com/74hc595/68k-nano/tree/master)
- 68HC000 12 MHz
- 1 MB RAM
- 64 kB ROM
- 16550 UART - TL16C550
- 44 pin IDE CF
- modern RTC module
- Fuzix OS supports it

[Blitz](https://github.com/ProbablyNotArtyom/Blitz)
- 68030 25 MHz
- FPU
- DRAM
- PS/2 keyboard
- ATA interface
- 3x ISA slot
- CPLD XC9572XL
- OS: G-DOS or Linux

## HW
### CPU
- MC68030FE SMD variant
	- cheaper than ceramic
	- €15-€20 on AliExpress, not available on LCSC
	- 16, 20, 25 MHz variants
	- 32 bit address and data
	- 25 MHz variant (SMD variant):
		- 5V, max 7V
		- 2.6 W max - 0.52 A
- DragonBall 68328
	- made for Palm, many integrated things
	- no MMU
	- easy bootable:
		- 32.768 kHz clock
		- ground nEMUBKT while resetting
		- has UART boot ROM
- MC68306
	- MC68EC000 core - no MMU
	- DRAM controller (up to 16/64 MB), interrupts, JTAG, timer, dual UART

### SRAM
- no DRAM DIMM/SIMMs (for now)
- 5V SRAM
- 16 bit
	- possible to to have 4x x8 instead of 2x x16
- 25 MHz - 40 ns
- 2x 1024 kB or 4x 512 kB

- AS6C8016
	- 1 MB
	- 16 bit
	- 55 ns - 18.18 MHz
	- dual SRAM
	- 19 address lines
	- 16 bit data output lines
	- others: CE, WE, OE, low byte ctrl, high byte ctrl
	- 2.7 - 5.5V
	- €9 LCSC NA
	- €19/5 AliExpress
- AS7C4098A
	- 512 kB
	- 16 bits
	- €5 LCSC NA
- IS61C25616AL
	- 512 kB
	- 16 bit
	- 12 ns - 83 MHz
	- €5 LCSC
- IS61C5128 AS/AL
	- 512 kB
	- 8 bits
	- has 10 ns (100 MHz) AL model
	- low power AS model
	- 8 bits - used in min 68010 boards?
	- €6 LCSC available

### flash
- AM29F040
	- used in [Computie K30v2](https://github.com/transistorfet/computie/)
	- 512 kB
	- 8 bit
	- 55 ns (18 MHz)
	- PLCC, DIP, TSOP (wide) packaging
	- not available on LCSC
	- €6 on AliExpress
- SST39SF040
	- 512 kB
	- 5V
	- 55/70 ns (14-18 MHz)
	- used in Mackerel
	- €3 LCSC NA

### UART
- MC68681
	- DIP40
	- €3 on AliExpress, not available on LCSC
- XR68C681
	- PLCC-44
	- €5 on AliExpress, not available on LCSC
	- needs
		- 8 data lines
		- 4 address lines
		- clock 3.6864 MHz
	- timer - used for CPU scheduling in Computie
	- not only 2x UART, it also contains:
		- 6 bit input
		- 8 bit output
- MC6850 ACIA/MC68B50
	- DIP24
- TL16C550
	- 16550 style UART
- TL16C2552
	- 16550 style dual UART
	- PLCC-44 packaging
	- €10 at LCSC, not available
- CPLD variant
	- [Simple 010](https://github.com/harrowm/Simple010) uses ATF1508 with MC68681 UART

### power
- 5V
	- CPU		MC68030FE	520 mA max
	- SRAM		AS6C8016	2x60 mA max (30 mA typical)
	- flash
	- serial

### later
- storage
	- IDE/CF
		- add [resistors](https://www.retrobrewcomputers.org/doku.php?id=boards:sbc:tiny68k:tiny68k_rev2) to the data lines. According to that sch:
			- D0..D15 - 100R serial
			- D9..D15 - 4.7k PU R - without D8
			- IORD 100R serial, 100 pF PD
		- CF card
			- socket available on LCSC
			- not available on LCSC
			- €25 for 8 GB on Amazon.de
			- €18 for SD -> CF adapter
	- SD
		- definitely more practical than CF
		- FC1306T: SD to IDE/CF
			- used by [Atari community](https://www.atari-wiki.com/index.php?title=Atari_Falcon_Flash_Media_Compatibility_Table)
- periph/GPIO
	Intel 8255 PPI - Programmable Peripheral Interface
	- 3x8 GPIO
	- per port configuration of input/output
	Motorola 6820/6821 PIA - Peripheral Interface adapter
	- 2x8 GPIO
	- per pin configuration
	- interrupts
	- [stack exchange](https://electronics.stackexchange.com/questions/678427/mc6820-pia-operation-on-the-apple-1)
- JTAG - or some way to debug and single step it
- CPLD: ATF150x
	- (open source)[https://whitequark.github.io/prjbureau/intro.html]
	- 3.3V ASV model (€9 LCSC)
	- 5V AS model (€18 LCSC)
	- (LCSC ATF1508 ASV)[https://www.lcsc.com/product-detail/C1521208.html]
		- QFP 14x14 mm
		- 128 macro cells
	- supported already by yosys?
	- [Playground 68030 Mk I](https://github.com/thorpej/pg68k/tree/main/cpu030)
		- 3x ATF1508AS: SYSCTL, DRAMCTL, ISACTL
- SPI
	- for uSD card, LAN
- I2C
	- for RTC
	- PCF8584: I2C master and slave
- keyboard, mouse
	- PS/2, but it will need MCU or parallel to PS/2
	- VT82C42
		- PS/2 controller for keyboard and mouse
		- used in Blitz 68030
- monitor
	- ISA VGA card
- FPU: MC68882
- USB host: WCH CH376S
	- 8 bit parallel or SPI or UART
	- read/write FAT32 from USB stick or SD card
- misc
	- timer: MC6840
	- multifunctonal peripheral: MC68901
		- 8x GPIO with interrupt
		- 4x timer
		- UART

#### misc
https://oldcpusrus.xepb.org/68k.html

## HW my
- multiple 100x100 mm PCBs
- (try) 2 layer PCB
- board interconnects:
	- 2x16 addr pin header
	- 2x16 data pin header
	- power
	- misc ctrl
		- 27 signals
		- 9 optional or NC signals (on Computie)
- PCBs:
	- CPU + SRAMs + flash + clk + reset button
		- LEDs on addr and data lines?
	- UARTs + USB UARTs + USB hub + PWR in
	- address decoders
		- discrete logic?
		- CPLD?
	- IDE: CF with optional uSD adapter
	- SMD parts, put passives at bottom, chips at top for aesthetics

## SW
- M68k after reset expects
	0x0000_0000  initial stack pointer
	0x0000_0004  initial PC
- vector table: 1 kB, 256 vectors
	- start address depends on VBR register, initially 0x0
- NetBSD support for thorpej Phaethon 1
	[Phaethon 1](https://github.com/thorpej/pg68k/blob/main/cpu010/README.md)
	- 68010 with custom MMU
	[NetBSD pull request](https://cvsweb.netbsd.org/bsdweb.cgi/src/build.sh?rev=1.403;content-type=text%2Fx-cvsweb-markup)
