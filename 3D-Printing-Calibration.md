# How To Calibrate Your 3D Printer Properly

### General Links

* Tom Sanladerer's Guides - https://www.youtube.com/playlist?list=PLDJMid0lOOYnRCAdbFfzECor3EbqF8euw
* Maker's Muse 3D Printing 101 - https://www.youtube.com/playlist?list=PLTCCNNvHC8PDR_jQy609toqq8EAfhiOOL
* RepRap Wiki - http://reprap.org/wiki/

### Stepper Driver Current

* When to Calibrate: During initial setup, when changing motor, stepper driver, or control board

**Don't calibrate stepper driver current with the motors plugged in!** If you set the current to the wrong value, you risk frying the driver or motor or both. Don't unplug the motors with the printer powered on either.

Power off your printer, unplug the motors, turn on the printer, and tune the drivers.

When finished, power off the printer, plug the motors back in, and turn on the printer.

Look up the formula for your stepper drivers. Some common ones:

* A4988: `V = A * (8 * R)` which is also `A = V / (8 * R)`
* DRV8825: `V = A * (5 * R)` which is also `A = V / (5 * R)`
* TMC2100: `V = A / (1.77 / 2.5)` which is also `A = V * (1.77 / 2.5)`

Basic tables for each driver are given on my [Stepper Motors and Drivers page](https://github.com/superjamie/lazyweb/wiki/3D-Printing-Stepper-Motors-and-Drivers).

Set your multimeter to DC voltage (2V). Measure voltage between DC negative of the power supply, and positive to the adjustment trimpot on the driver board. A good tip is to use multimeter clamps, so you clamp one to the negative on the power supply, and positive to your screwdriver. Then the screwdriver can measure voltage at the trimpot as you adjust it.

Look up the current of your motors, set to that current or just under it. You may be able to get away with 80% less current depending on setup. If you have very powerful motors like 70Ncm you can set the motors to way less torque to keep them cool.

Current and torque do not scale linearly, reducing current by 20% can reduce torque by 40% or more. If you find you're skipping motor steps *and everything else is mechanically good* then you could try increase motor current to avoid the skipped steps. If you have a mechanical problem, don't just increase stepper driver current to power through it, solve the mechanical problem properly.

I find the extruder needs more torque than the motion axes. This makes more sense as it's easier to move a carriage sliding over smooth and lubricated rods/rails/wheels than it is to force millimeters of filament through a very tiny nozzle hole. A geared extruder can help avoid the need for such a powerful filament motor.

References:

* https://github.com/superjamie/lazyweb/wiki/3D-Printing-Stepper-Motors-and-Drivers
* http://reprap.org/wiki/A4988_vs_DRV8825_Chinese_Stepper_Driver_Boards
* http://reprap.org/wiki/Stepper_motor
* [Tom Sanladerer - 3D printing guides - How steppers work and how to adjust their drivers](https://www.youtube.com/watch?v=bItYRMLGoVc)

### XYZ Steps

* When to Calibrate: During initial setup, when changing axis gear/motor/parts

The correct figures for X, Y, and Z axis are based on physical properties of your printer. You don't "tune" or adjust these unless you change parts.

The correct way to determine these values is to find your motor's step angle (usually 1.8° or 0.9°), the microstepping of your drivers (usually 1/16 or 1/32), your belt pitch (2mm for GT2), and either the number of teeth on your pulleys (usually 16, 20, or 36) or the pitch of your leadscrew (usually 2mm or 8mm).

The formulas are given on Triffid Hunder's calibration guide, but the Prusa Calculator makes this very easy, so just use that.

These are your "Steps Per mm" values to be entered into the firmware, eg:

~~~
1.8 deg motor, 1/16 microstep, GT2 belt, 20T pulley = 80 steps/mm
1.8 deg motor, 1/16 microstep, 2mm leadscrew = 1600 steps/mm

#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 1600, E }
~~~

References:

* http://www.prusaprinters.org/calculator/
* http://www.reprap.org/wiki/Triffid_Hunter's_Calibration_Guide
* [Tom Sanladerer - 3D printing guides: Calibration and why you might be doing it wrong](https://www.youtube.com/watch?v=Mbn1ckR86Z8)

### Extruder Steps

* When to Calibrate: During initial setup, when changing extruder motor/parts, when changing filament material

You can do a rough calculation for extruder steps based on the diameter of the gear, or just set to `100` and test from there.

If you're using a geared extruder then multiply that start value by the gear ratio.

Mark the filament at the entrance to the extruder, tell the printer to extrude 100mm, then mark where the filament stops.

Remove the filament, measure between the two marks. Now adjust the E steps per mm by the following calculation:

~~~
new_e_steps = old_e_steps * (100 / distance_actually_moved)
~~~

Now do it again. Mark, extrude, mark, measure.

When you tell the printer to extrude 100mm and the measurement between the marks is actually 100mm, you've calibrated correctly.

This goes as the last measurement:

~~~
#define DEFAULT_AXIS_STEPS_PER_UNIT   { X, Y, X, 100 }
~~~

Different filament (eg: PLA vs PETG) will likely be gripped differently by the gear as the teeth "dig in" more or less, which modifies the effective diameter of the pulley and hence modifies the ideal steps. You can set the value in the start G-code for a material like `M92 E101`

References:

* [Tom Sanladerer - 3D printing guides - Calibrating your extruder](https://www.youtube.com/watch?v=YUPfBJz3I6Y)
* http://zennmaster.com/makingstuff/reprap-101-calibrating-your-extruder-part-1-e-steps
* http://reprap.org/wiki/G_code#M92:_Set_axis_steps_per_unit

### Speeds

* When to Calibrate: During initial setup, when changing mechanical/weight properties of the printer.

~~~
TODO - make nicer
~~~

tl;dr - don't try and print too fast

start with XY max 250, XY accel 1000, XY jerk 4, print speed 40mm/sec

work up from there

accel 1500 is very good. jerk should be 10% of print speed or less

different materials require different print speeds, so tune speed with PLA (or whatever you print with most often)and just tell the slicer to print slower for other materials as required

* https://www.thingiverse.com/thing:277394
* [Tom Sanladerer - 3D printing guides - Tuning speeds](https://www.youtube.com/watch?v=7HsIZuj9vOs)
* [Tech2C - This is Y](https://www.youtube.com/watch?v=AKTvykTPjQw)

### Firmware Temperature

* When to Calibrate: When changing thermistor, when changing printer location, when changing environmental conditions (eg: cold winter, hot summer)

Set up the right Thermistor in the firmware.

Do PID Autotune of your nozzle and bed from cold. Tune under regular running conditions, like if you use a silicone sock and a fan on the hotend, have both of those on. If you use a glass or PEI sheet, have that clamped to the bed too.

`M303 E0 S200 C8` for nozzle, and `M303 E-1 S60 C8` for bed.

Different firmware uses different IDs for nozzle and bed:

* Marlin: `E0` and `E-1`
* Repetier: `P0` and `P3`
* Smoothieware: `E0` and `E1`

References:

* [Tom Sanladerer - 3D printing guides - Using Marlin's PID autotune](https://www.youtube.com/watch?v=APzJfYAgFkQ)

### Filament Temperature

* When to Calibrate: When using a different brand, color, or material of filament for the first time

~~~
TODO - make nicer
~~~

print a temperature tower, find one on Thingiverse

change temperature as you print it, corresponding with the designs on the tower. in Cura use the TweakAtZ plugin in Postprocessing. in S3D use multiple processes covering a height range and change the temperature in each process. slic3r cannot do this directly, so you need to edit the gcode or babysit the print and tweak the temperature manually via LCD or host program

once you have it printed, pick which temperature looks best or gives the strongest layer adhesion or the best detail or the best bridging or whatever aspect you care about

for pla use 185c to 235c

for petg use 200c to 250c

* https://www.thingiverse.com/search?q=temperature+tower
* https://www.thingiverse.com/search?q=temperature+calibration

### Filament Diameter

* When to Calibrate: For each filament spool

Being sure to keep tension on the roll so it doesn't unwind in a big mess, pull a couple of meters out of the filament roll and measure the diameter along various points and around various angles.

Take note of all these measurements and find the average, this is the value you put into the slicer for filament width.

If the filament varies by more than 0.01mm either way (eg: the average is 1.71mm but varies more than 1.70 and 1.72 along or around), or is larger than 1.76mm anywhere, then return it as faulty.

### Extrusion Flow Rate

* When to Calibrate: For each filament spool, for each extrusion width, when changing nozzle

In your slicer, set your extrusion width to your nozzle diameter or up to 120% of it. If you have a 0.4mm nozzle, then set to 0.4mm or 0.48mm or anywhere in between.

Download or make a 20mm cube and print it with 1 wall and no top layers.

Using Cura's TweakAtZ or Simplify3D multiple processes, change the flow rate so the bottom 4mm print at 110%, the next 4mm above that print at 105%, the next 4mm above that at 95%, and so on. You can stretch the cube in the Z direction if you wish to use smaller steps (like 2.5%) or test more flow rates.

Once this is printed, use your measuring calipers to measure the actual extrusion width at each height when the flow rate changed. It likely won't be exactly the width you specified, so calculate an extrusion flow rate similar to calculating extrusion steps:

~~~
new_flow_rate = (width_in_slicer / actual_width) * 100
~~~

Finally, set your flow rate to that number and try a single print again without Z height changes. If you can get within 0.01mm I think that's good enough.

* http://print.theporto.com/posts/how-to-calibrate-extrusion-thickness/
* http://zennmaster.com/random-things/reprap-101-calibrating-your-extruder-part-2-fine-tuning
* https://solidoodletips.wordpress.com/2012/08/16/setting-the-flow-rate/

## Stringing, Bridging, Retraction

* When to Calibrate: When using a different brand, color, or material of filament for the first time

~~~
TODO - make nicer
~~~

print some torture tests

futz with the settings like print speed, retraction, coast, cooling until you get good print quality

* https://www.thingiverse.com/thing:2219103

## Print Quality Troubleshooting

You don't need to remember these all off the top of your head. Skim the pictures and look for poor aspects of printing which you should watch for in your prints.

If you ever have a print problem, go through these guides and try the suggestions within:

* http://support.3dverkstan.se/article/23-a-visual-ultimaker-troubleshooting-guide
* https://www.simplify3d.com/support/print-quality-troubleshooting/
* http://deltaprintr.com/troubleshooting/
* http://builda3dprinter.eu/information/troubleshooting-guide/
* https://all3dp.com/1/common-3d-printing-problems-troubleshooting-3d-printer-issues/
* http://reprap.org/wiki/Print_Troubleshooting_Pictorial_Guide

## Maintenance / Service

Every Print

* Inspect axis belts/rods/rails/slots for any random plastic pieces and remove
* Remove any debris off print bed
* If using build surface, clean build surface by wiping with isopropyl alcohol
* If using adhesive (glue/hairspray), ensure material is level and there's enough on there
* Clean boogers off nozzle as the print starts

Weekly or Fortnightly

* Level bed manually (even if you're using auto levelling)

Monthly or when a roll of filament runs out

* Check belt tension, use a sound meter on your phone to tune around 41Hz
* Clean rods
* Lubricate rods/screws/bearings
* Blow dust out of fans
* Blow dust out of filament gear
* Check/clean/replace [filament dust filter](https://www.thingiverse.com/thing:497764)
* Check nozzle bore to ensure nozzle isn't wearing out/down too much

Quarterly

* Check set screws on motor pulleys, couplers, extruder gear
* Check screws holding in all frame, motors, rods, and other mounted parts
* Inspect Bowden tube and trim/replace if required
* Clean nozzle using [cold pull](https://printrbot.zendesk.com/hc/en-us/articles/202100554-Unclogging-the-Hotend-using-the-Cold-Pull-method) aka [atomic method](https://ultimaker.com/en/resources/19510-how-to-apply-atomic-method)
* Ensure nozzle is fastened against heatbreak while hot
* Update firmware
* Update host software

References

* https://www.lulzbot.com/maintaining-your-3d-printer
* https://www.youtube.com/watch?v=SdXT_SR8dC8
* http://support.3dverkstan.se/article/42-basic-maintenance
* https://pinshape.com/blog/3d-printer-maintenance/
* https://ultimaker.com/en/resources/21925-maintaining-your-printer
* http://zx3d.com.au/maintenance/
* https://www.makerbot.com/media-center/2011/01/27/how-to-get-better-results-from-your-3d-printer-%E2%80%93-part-iv
