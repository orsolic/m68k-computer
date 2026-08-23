# HW

List of HW parts which were evaluated for use on this project.

## CPU
- MC68030FE SMD variant
	- cheaper than ceramic
	- €15-€20 on AliExpress, not available on LCSC
	- 16, 20, 25, 33 MHz variants
	- 32 bit address and data
	- 25 MHz variant (SMD variant):
		- 5V, max 7V
		- 2.6 W max - 0.52 A

- DragonBall 68328
	- made for Palm, many integrated things
	- no MMU
	- [easy bootable](https://hackaday.io/project/36309-melting-the-balls-off-the-dragonball/log/78851-the-tiniest-minimalist-68k):
		- 32.768 kHz clock
		- ground nEMUBKT while resetting
		- has UART boot ROM

- MC68306
	- MC68EC000 core - no MMU
	- DRAM controller (up to 16/64 MB), interrupts, JTAG, timer, dual UART

## SRAM
- no DRAM DIMM/SIMMs (for now)
- 5V SRAM
- 16 bit
	- possible to to have 4x x8 instead of 2x x16
- 25 MHz - 40 ns

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

## ROM
- flash EEPROM used as ROM
- 8-bit data access - will help up with address decoding
- not speed critical, only startup code will be on it

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

## UART
- MC68681
	- 2x UART
	- DIP40
	- from 1985
	- €3 on AliExpress, not available on LCSC
	- 115,200 kbps capable
	- better/newer variant of UART in MFP MC68901

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

- MC68901
	- [max 9600 bps](https://hackaday.io/project/164305-roscom68k/log/184878-mc68681-spi-lcds-and-sd-cards-an-overdue-update)
	- [not that great](https://hackaday.io/project/164305-roscom68k/log/178889-dramatically-improving-comms-speed.htm)

- SC26C94
	- 4x UART used in Aslak's MAXI030
	- not available on LCSC

## oscillator
- 12-25 MHz
- 5V
- crystal can be TH 2-pin or SMD 2-pin or SMD 4-pin
- oscillator is SMD 4-pin with VCC pin

## power
- 5V
	- CPU		MC68030FE	520 mA max
	- SRAMs		AS6C8016	2x60 mA max (30 mA typical)
	- ROM
	- UART
	- SN74xx

## storage
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

## periph/GPIO
- Intel 8255 PPI - Programmable Peripheral Interface
	- 3x8 GPIO
	- per port configuration of input/output

- MC6820/MC6821 PIA - Peripheral Interface adapter
	- 2x8 GPIO
	- per pin configuration
	- interrupts
	- [stack exchange](https://electronics.stackexchange.com/questions/678427/mc6820-pia-operation-on-the-apple-1)
- MC68901
	- multifunctonal peripheral: vectored interrupts, PIT, GPIO with int, UART
	- from 1983/1984
	- 8x GPIO with interrupt
	- 4x timer
	- UART

- MC68230 PIT - Parrallel Interface/Timer

- MCP23017
	- used in J4F "KIT 68K-MBC" with 68008
	- i2c to 16 GPIO

- W65C22
	- 2x8 GPIO, individual I/O config
	- 2x 16b timer

## JTAG - or some way to debug and single step it
- JTAG is newer than 68k
- single stepping with discrete logic?

## chipset
- CPLD: ATF150x
	- for creating memory map, address decoding and CS signal selecting
	- [open source](https://whitequark.github.io/prjbureau/intro.html)
	- 3.3V ASV model (€9 LCSC)
	- 5V AS model (€18 LCSC)
	- [LCSC ATF1508 ASV](https://www.lcsc.com/product-detail/C1521208.html)
		- QFP 14x14 mm
		- 128 macro cells
	- supported already by yosys?
	- [Playground 68030 Mk I](https://github.com/thorpej/pg68k/tree/main/cpu030)
		- 3x ATF1508AS: SYSCTL, DRAMCTL, ISACTL

- MCU chipset
	- not for address decoding, more like southbridge, for lower speed peripherals
	- UART IC will be hard to find
	- STM32 will be already used as (external) ROM programmer
	- 8 pins (5V tolerant) for data
	- 2-3 pins for register select
	- GPIO
	- SPI
	- I2C
	- I2S audio
	- PS/2 interface
	- USB

## SPI
- uSD card
- LAN

## I2C
- for RTC
- PCF8584
	- I2C master and slave

## keyboard, mouse
- PS/2, but it will need MCU or parallel to PS/2
- VT82C42
	- PS/2 controller for keyboard and mouse
	- used in Blitz 68030

## monitor
- ISA VGA card
- [Xark Xosera](https://github.com/XarkLabs/Xosera)
	- iCE40 FPGA - open source toolchain
	- [Rosco m68k with Xosera](https://hackaday.io/project/164305-roscom68k/log/192206-xosera-vga-on-roscom68k)

## sound card
- ISA card?

## DMA
- MC68450
	- not available on AliExpress
	- eBay: €25 + €6

## FPU
- MC68881/MC68882

## USB host
- WCH CH376S
	- 8 bit parallel or SPI or UART
	- read/write FAT32 from USB stick or SD card

## LAN
- SPI or parallel
- RTL8019AS
	- 10€ at LCSC
	- 20 bit address
	- 16 bit data

## IC for supervision
- [BQ4845 - supervision and RTC](https://www.ti.com/product/BQ4845)
	- almost obsolete
- [DS1233](https://www.analog.com/en/products/ds1233.html)
	- monitors voltage
	- asserts RESET and holds it for 350 ms
	- 3 pin device (and large)
	- €3 at LCSC
- DS1813
- ADM705/706/707/708
	- watchdog and power supervision

## timer
- MC6840
- XR68C681
	- mainly dual UART with timer
