# Software

Final goal of this project will be to run NetBSD on it.

## Generic
- M68k after reset expects  
	0x0000_0000  initial stack pointer  
	0x0000_0004  initial PC  
- vector table: 1 kB, 256 vectors  
	- start address depends on VBR register, initially 0x0  

## Toolchain
- Debian toolchain should be one apt install away
- [ddraig68k](https://github.com/ddraig68k/m68k-elf-toolchain)

## ROM monitors
- WozMon 68k

## OS
- [CP/M](https://en.wikipedia.org/wiki/CP/M)
	- written by Gary Kildall
	- [CP/M-68k](http://www.retroarchive.org/docs/software/cpm68.html)
	- [on s100](https://www.s100computers.com/Software%20Folder/CPM68K/CPM68K%20Software.htm) [github](https://github.com/dwildie/cpm-68k)
	- [misc](https://www.davesrocketworks.com/electronics/cpm68/index.html)

- [Amiga TOS OSS clone](https://emutos.sourceforge.io/)
	- [github](https://github.com/emutos/emutos)
	- "It can run on real hardware as a ROM replacement, bootable floppy, standard executable, cartridge..."

- NetBSD
	- requirements [hp300](https://wiki.netbsd.org/ports/hp300/)
		- supports '020, '030, '040
		- 4 MB of RAM minimal
		- 8 MB of RAM recommended
	- hb68k
		- homebrew 68k
		- no link yet
		- Wire030 is supported since [2026.08.](https://github.com/NetBSD/src/commit/ef5da7a89e0be453cd8cef0cf5713e547240dbad)
		- uses [FDT](https://github.com/NetBSD/src/blob/trunk/sys/arch/hb68k/wrap030/wrap030.dts)
		- [Phaethon 1](https://github.com/thorpej/pg68k/blob/main/cpu010/README.md) (68010 with custom MMU) [supported](https://cvsweb.netbsd.org/bsdweb.cgi/src/build.sh?rev=1.403;content-type=text%2Fx-cvsweb-markup)
	- [NetBSD cmmc68 (fork)](https://github.com/ChrisPVille/NetBSD-cmmc68)
		- port of NetBSD for '010 with custom MMU

- [Debian](https://www.debian.org/ports/m68k/)
	- needs MMU
	- works without FPU
	- latest official is 4.0 Etch

## OS custom
- [Gloworm](https://github.com/transistorfet/gloworm)  
	- written in C
	- inspired by Tanenbaum's book, but not micro kernel
	- from the person who designed Computie K30
	- [monitor](https://github.com/transistorfet/gloworm/tree/main/src/monitor)
	- [docs](https://jabberwocky.ca/projects/gloworm/)
