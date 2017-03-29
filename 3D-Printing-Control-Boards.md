## RAMPS

* http://reprap.org/wiki/RAMPS_1.4

Designed for use with Arduino Mega 2560 8-bit CPU. Accepts 12V power input.

#### Firmware

* Marlin - http://www.marlinfw.org/
* Repetier Firmware - https://www.repetier.com/firmware/v092/

## RAMPS-FD

* http://www.reprap.org/wiki/RAMPS-FD

Designed for use with Arduino Due (3.3v TTL) 32-bit CPU, but also works on Mega 2560.

Apparently the RAMPS-FD v1.x has safety concerns, Geeetech sold the unfinished pre-release design despite being asked not to.

bobc designed RAMPS-FD v2.2 but gave up the project, and all the Chinese sellers still sell v1.

Fixes for v1 boards are detailed at: http://forums.reprap.org/read.php?219,424146

#### Firmware

* RepRapFirmware: http://reprap.org/wiki/RepRap_Firmware

## MKS Boards

All accept 12V to 24V power input. Not open source.

Makerbase reverse the EXT1 and EXT2 LCD connectors so you need to shave the tabs off LCD cables and reverse them if not using MKS-branded LCD2004 (RRD Smart Controller) or LCD12864 (RRD Full Graphic Smart Controller).

MKS have cases for all of these on their GitHub: https://github.com/makerbase-mks/MKS-STL

### BASE

2560 8-bit and RAMPS in one, built-in A4982 stepper drivers and no way to run external drivers.

### GEN

2560 8-bit and RAMPS in one, 16-pin Pololu stepper sockets so can use any driver.

### SBASE

* https://github.com/makerbase-mks/MKS-SBASE

Clone of 32-bit Smoothieboard. Arthur Wolf [fucking hates them](http://forums.reprap.org/read.php?13,499322). Built-in DRV8825 stepper drivers with a jumper to run 1/16 or 1/32. Also has 4 pins to run external drivers if desired. Have seen someone running TMCs. Check Makerbase's GitHub for an example config, some of the pinouts for motors, fan, temperature, panel and sdcard SPI channel are different to Smoothieboard.

~~~
TODO: Document non-default pinouts
~~~

### Firmware

* Smoothieware: http://smoothieware.org/

## DuetWifi

* https://www.duet3d.com/DuetWifi
* http://reprap.org/wiki/DuetWifi

All-in-one Arduino Due 32-bit board. Accepts up to 25V input. Five built-in TMC2660 stepper drivers.

#### Firmware

* RepRapFirmware: http://reprap.org/wiki/RepRap_Firmware