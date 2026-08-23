# Examples

Examples of M68k homebrew computers made by others, which were used as a learning platform and inspiration.  

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
- 12 MHz clock (for 12 MHz variant of the chip)

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

[PG68k](https://github.com/thorpej/pg68k)
- multiple designs
- Phaethon 1
	- MC68010 with custom MMU
	- NetBSD capable
	- no DMA
- cpu030
	- MC68030
	- 2x DRAM
	- ATA drive
	- 3x CPLD: ATF1508AS
- JTAG?

[Jackalope MC68030 Board](https://retrobrewcomputers.org/doku.php?id=dev:boards:jackalope_68030:start)
- FPU
- DRAM: SIMM 72
- CPLD:

[M68K-MBR](https://j4f.info/68k-mbc)
- 68008, has kit for €90
- [(bad) schematics - multiple .pdf files](https://github.com/GeraKuznetsov/M68K-MBC)
- PIC MCU (
- (untested) PLL with discrete logic

[Rosco M68K](https://hackaday.io/project/164305-roscom68k)
- MC68010
- [many logs](https://hackaday.io/project/164305/logs?sort=oldest)

[Rosco M68k Pro](https://hackaday.io/project/180929-roscom68kpro)
- MC68030 CPU
- 4x SRAM AS6C4008
- 4x ROM
- incorporated into main Rosco M68k
- [hackaday logs](https://hackaday.io/project/180929-roscom68kpro/log/198890-first-prototype-out-for-production)

[Wrap030](https://github.com/techav-homebrew/Wrap030)
- MC68030
- NetBSD in-tree support, [fork](https://github.com/techav-homebrew/netbsd-wrap030)
- [docs](https://techav.net/tagged/wrap030/page/3)
- FPU
- ATX connector for PSU

[Wrap030 ATX](https://github.com/techav-homebrew/Wrap030-ATX)
- [docs](https://techav.net/post/714948735442010112/introducing-wrap030-atx)
- MC68030
- FPU
- 2x DRAM slot
- 3x ISA slot
- IDE hard drive
- PS/2 keyboard

[Stuart 68k](https://hackaday.io/project/7242-motorola-68000-computer)
- [github](https://github.com/stuartatpeasy/m68k-system)
- 68010 but with [interesting](https://hackaday.io/project/7242/logs?sort=oldest) peripherals
- [homebrew OS](https://github.com/stuartatpeasy/m68k-system/tree/master/ayumos)
- nice motherboard
- tries to be period complete
- nice connectors for [bus](https://hackaday.io/project/7242/log/30087-expansion-interface)
- [LAN card](https://hackaday.io/project/7242-motorola-68000-computer/log/28291-10100mbps-ethernet-card) with [ENC624J600](https://ww1.microchip.com/downloads/en/DeviceDoc/39935b.pdf)
	- Olimex has something [similar](https://www.olimex.com/Products/Modules/Ethernet/MOD-ENC624J600/)
- [PS/2 interface](https://hackaday.io/project/7242-motorola-68000-computer/log/29957-mc68000-ps2-keyboard-mouse-interface) based on ATmega8
