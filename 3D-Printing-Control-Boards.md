# Control Boards

## 8-Bit Arduino

### Firmware

* Marlin - http://www.marlinfw.org/
* Repetier Firmware - https://www.repetier.com/firmware/v092/

### Arduino Mega 2560 + RAMPS

* http://reprap.org/wiki/RAMPS_1.4

Accepts 12V power input.

### MKS BASE and GEN

All accept 12V to 24V power input. Not open source.

Makerbase reverse the EXT1 and EXT2 LCD connectors so you need to shave the tabs off LCD cables and reverse them if not using MKS-branded LCD2004 (RRD Smart Controller) or LCD12864 (RRD Full Graphic Smart Controller).

MKS have cases for all of these on their GitHub: https://github.com/makerbase-mks/MKS-STL

#### BASE

All-in-one Mega 2560 and RAMPS. Built-in A4982 stepper drivers and no way to run external drivers.

#### GEN

All-in-one Mega 2560 and RAMPS. 16-pin Pololu stepper sockets so can use any driver.

## 32-bit Smoothieboards

### Firmware

* Smoothieware: http://smoothieware.org/

### Smoothieboard

Original Smoothieware board, the Smoothie community like and support these.

* http://smoothieware.org/smoothieboard

### Azteeg X5

* https://www.panucatt.com/azteeg_X5_GT_reprap_3d_printer_controller_p/ax5gt.htm
* https://www.panucatt.com/azteeg_X5_mini_reprap_3d_printer_controller_p/ax5mini.htm

Smoothie community like and support these.

### Re-ARM for RAMPS

* https://www.panucatt.com/Re_ARM_for_RAMPS_p/ra1768.htm

Runs Smoothieware but is in the same form factor as Mega 2560 and can use RAMPS.

Originally a Kickstarter project but now available for general sale.

Smoothie community like and support these.

### MKS SBASE

* https://github.com/makerbase-mks/MKS-SBASE

Closed source clone of Smoothieboard. Arthur Wolf [fucking hates them](http://forums.reprap.org/read.php?13,499322).

Five built-in DRV8825 stepper drivers with a jumper to run 1/16 or 1/32. Also has 4 pins to run external drivers if desired. Have seen someone running TMCs. Check Makerbase's GitHub for an example config, some of the pinouts for motors, fan, temperature, panel and sdcard SPI channel are different to Smoothieboard.

~~~
TODO: Document non-default pinouts
~~~

* v1.2 fixed the heatbed
* v1.3 fixed the Ethernet crystal

## 32-bit Arduino Due

### Firmware

* RepRapFirmware: http://reprap.org/wiki/RepRap_Firmware

### Arduino Due and RAMPS-FD

* http://www.reprap.org/wiki/RAMPS-FD

RAMPS-like shield designed for use with Arduino Due (3.3v TTL) 32-bit CPU, but also works on Mega 2560.

Apparently the RAMPS-FD v1.x has safety concerns, Geeetech sold the unfinished pre-release design despite being asked not to.

bobc designed RAMPS-FD v2.2 but gave up the project, and all the Chinese sellers still sell v1.

Fixes for v1 boards are detailed at: http://forums.reprap.org/read.php?219,424146

### DuetWifi

* https://www.duet3d.com/DuetWifi
* http://reprap.org/wiki/DuetWifi

All-in-one Arduino Due and support circuitry. Accepts up to 25V input. Five built-in TMC2660 stepper drivers.
