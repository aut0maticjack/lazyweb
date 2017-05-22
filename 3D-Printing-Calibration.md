# How To Calibrate Your 3D Printer Properly

General Links

* Tom Sanladerer - https://www.youtube.com/channel/UCb8Rde3uRL1ohROUVg46h1A
* RepRap Wiki - http://reprap.org/wiki/

## Stepper Driver Current

~~~
TODO
~~~

do this before plugging in. power off and unplug motors before tuning

look up the formula for your stepper drivers

set your multimeter to DC voltage (2V), clamp negative to the power supply ground, and positive to your screwdriver, measure at the trimpots as you adjust

look up the current of your motors, set to that current or just under it. you may be able to get away with 80% less current depending on setup

current and torque do not scale linearly, reducing current by 20% can reduce torque by 40% or more

i find the extruder needs more torque than the motion axes

References:

* http://reprap.org/wiki/A4988_vs_DRV8825_Chinese_Stepper_Driver_Boards
* http://reprap.org/wiki/Stepper_motor
* [Tom Sanladerer - 3D printing guides - How steppers work and how to adjust their drivers](https://www.youtube.com/watch?v=bItYRMLGoVc)

## XYZ Steps

The correct figures for X, Y, and Z axis are based on physical properties of your printer. You don't "tune" or adjust these unless you change parts.

The correct way to determine these values is to find your motor's step angle (usually 1.8° or 0.9°), the microstepping of your drivers (usually 1/16 or 1/32), your belt pitch (2mm for GT2), and either the number of teeth on your pulleys (usually 16, 20, or 36) or the pitch of your leadscrew (usually 2mm or 8mm).

The formulas are given on Triffid Hunder's calibration guide, but the Prusa Calculator makes this very easy, so just use that,

These are your "Steps Per mm" values to be entered into the firmware, eg:

~~~
1.8 deg motor, 20T pulley, 1/16 microstep, GT2 belt = 80 steps/mm
1.8 deg motor, 2mm leadscrew, 1/16 microstep = 1600 steps/mm

#define DEFAULT_AXIS_STEPS_PER_UNIT   { 80, 80, 1600, E }
~~~

References:

* http://www.prusaprinters.org/calculator/
* http://www.reprap.org/wiki/Triffid_Hunter's_Calibration_Guide
* [Tom Sanladerer - 3D printing guides: Calibration and why you might be doing it wrong](https://www.youtube.com/watch?v=Mbn1ckR86Z8)

## Extruder Steps

You can do a rough calculation for extruder steps based on the gear, or just set to `100` and test from there.

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

References:

* [Tom Sanladerer - 3D printing guides - Calibrating your extruder](https://www.youtube.com/watch?v=YUPfBJz3I6Y)
* http://zennmaster.com/makingstuff/reprap-101-calibrating-your-extruder-part-1-e-steps

## Speeds

~~~
TODO
~~~

* [Tom Sanladerer - 3D printing guides - Tuning speeds](https://www.youtube.com/watch?v=7HsIZuj9vOs)
* [Tech2C - This is Y](https://www.youtube.com/watch?v=AKTvykTPjQw)

## Temperature

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

## Filament Diameter

* When to Calibrate: For each filament spool

Being sure to keep tension on the roll so it doesn't unwind in a big mess, pull a couple of meters out of the filament roll and measure the diameter along various points and around various angles.

Take note of all these measurements and find the average, this is the value you put into the slicer for filament width.

If the filament varies by more than 0.01mm either way (eg: the average is 1.71mm but varies more than 1.70 and 1.72 along or around), or is larger than 1.76mm anywhere, then return it as faulty.

### Extrusion Flow Rate

* When to Calibrate: For each filament spool, and for each extrusion width

In your slicer, set your extrusion width to your nozzle diameter or up to 120% of it. If you have a 0.4mm nozzle, then set to 0.4mm or 0.48mm or anywhere in between.

Download or make a 20mm cube and print it with 1 wall and no top or bottom layers. Use "Vase Mode" if you like.

Use your measuring calipers to measure the actual extrusion width. It likely won't be exactly the width you specified, so calculate an extrusion flow rate like we did:

~~~
new_flow_rate = (width_in_slicer / actual_width) * 100
~~~

Now set your flow rate to that number and try a print again. If you can get within 0.01mm I think that's good enough.

* http://print.theporto.com/posts/how-to-calibrate-extrusion-thickness/
* http://zennmaster.com/random-things/reprap-101-calibrating-your-extruder-part-2-fine-tuning
* https://solidoodletips.wordpress.com/2012/08/16/setting-the-flow-rate/

## Stringing, Bridging, Retraction

~~~
TODO
~~~

* https://www.thingiverse.com/thing:2219103