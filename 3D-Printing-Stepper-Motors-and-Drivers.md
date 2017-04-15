# Stepper Motors

Learn how stepper motors work:

* https://www.youtube.com/watch?v=eyqwLiowZiU
* https://www.youtube.com/watch?v=bkqoKWP4Oy4

3D printers usually use NEMA17 motors which are 1.7" (43.2mm) square across the face. There are larger sizes like NEMA23 and NEMA34 which are common on CNCs. There are smaller sizes like NEMA14 and NEMA11 too. The first RepRap 3D printers used NEMA14s but they were right on the limit of what they could do well.

Look up your motor's part number and pay attention to the **Step Angle**, **Holding Torque**, and **Rated Current**.

3D printers need at least 40 N-cm holding torque. Generally the longer the motor the more torque it has, but not always, there are some "pancake steppers" specifically designed to be high-torque in a small light package.

Not everyone publishes in N-cm so check other stupid manufacturer measurements at a torque converter like: http://www.numberfactory.com/nf%20torque.htm

* 1 N-cm = 0.1019716 kg-cm, so 40 N-cm = 4.08 kg-cm
* 1 N-cm = 1.41612 oz-in, so 40 N-cm = 56.64 oz-in

I find my extruder needs more current (1A to 1.2A) than the XYZ motion motors (0.75A).

Use the Step Angle to work out motor steps for firmware with: http://www.prusaprinters.org/calculator/

## How to Tune

Turn power off, unplug the stepper motor cables, turn power back on and tune the stepper drivers.

When done, turn power off, plug in the stepper motor cables, turn power back on and test motor movement.

Don't tune stepper drivers with the motors plugged in, if you accidentally set current too high you can fry the motor.

Don't plug or unplug stepper motors with the power on.

Measure DC voltage between the stepper trimpot and 12V ground. The ground at the 12V supply to the control board is fine to use.

Look up the correct current for your motor part number. If you have cheap Chinese motors with no part number, assume they have a max of 1.25A to be safe.

Look up the proper formula for your stepper drivers below, and find the voltage which corresponds with the current you want to set.

Pro tip: Get slip-on alligator clips for your multimeter. Clamp ground to a 12V ground wire and clamp positive to your screwdriver. This way you'll measure the voltage as you adjust and don't need three hands.

## References

* http://reprap.org/wiki/Stepper_motor
* http://reprap.org/wiki/NEMA_17_Stepper_motor

# Stepper Motor Drivers

| Manufacturer      | Chip    | Max Microstep | Max Current | Datasheet |
|-------------------|---------|---------------|-------------|-----------|
| Allegro           | A4988   | 1/16          | 2A          | [PDF](http://www.allegromicro.com/~/media/Files/Datasheets/A4988-Datasheet.ashx?la=en) | 
| Texas Instruments | DRV8825 | 1/32          | 2.5A        | [PDF](www.ti.com/lit/ds/symlink/drv8825.pdf) |
| Sanyo             | LV8729  | 1/128         | 1.3A        | [Alldatasheet](http://www.alldatasheet.com/view.jsp?Searchword=LV8729)
| Trinamic          | TMC2100 | 1/256         | 1.25A       | [PDF](https://www.trinamic.com/fileadmin/assets/Products/ICs_Documents/TMC2100_datasheet.pdf) |

## A4988

The "default" choice. Work fine.

~~~
Formula: V = A * (8 * R)
Amps    Volts
1.7     1.36
1.3     1.04
1.2     0.96
1       0.8
0.8     0.64
		
Formula: A = V / (8 * R)
Volts   Amps
0.6     0.75
0.8     1
1       1.25
1.25    1.5625
1.5     1.875
		
Current Sense Resistor		
0.1
~~~

## DRV8825

Seem to be a good upgrade. Much stronger than A4988s to move the carriage against.

~~~
Formula: V = A * (5 * R)		
Amps    Volts
0.5     0.25
0.75    0.375
1       0.5
1.1     0.55
1.2     0.6
1.5     0.75
		
Formula: A = V / (5 * R)		
Volts   Amps
0.5     1
0.55    1.1
0.575   1.15
0.6     1.2
1       2
1.25    2.5

Current Sense Resistor
0.1
~~~

They get a high-pitched whine, apparently due to the supply voltage (12V) being larger than the motor voltage (typically 2.8V). Some people say to use 4.2V motors and this goes away. There is a circuit which can get rid of this, with ready-made PCBs sold on Aliexpress as "TL-Smoother". The circuit is explained at:

* http://www.engineerination.com/2015/02/drv8825-missing-steps.html

This page also discusses noise:

* http://ebldc.com/?p=187

As stated above, reducing current can also prevent the noise. For boards with digipots to adjust motor current, you could set the current high when printing, and low enough to hold the Z axis up when not printing, which would at least limit the noise. G-code to do this is in the format:

~~~
M907 X1.0 Y1.0 Z1.0 E1.5
~~~

* http://smoothieware.org/supported-g-codes

Apparently using a SilentStepStick Protector may help? See:

* http://forums.reprap.org/read.php?13,666367
* http://www.watterott.com/en/SilentStepStick-Protector

More research required on decay mode:

* https://www.youtube.com/watch?v=Wf8rN3bV8XM

## LV8729

Not much info out there on these. Supposed to be quiet.

Peak current 1.8A but constant max is advertised as either 1.3A or 1.5A.

* http://forums.reprap.org/read.php?160,724177

~~~
Formula: V = A * (0.5)	
Amps	Volts
1.5     0.75
1.3     0.65
1.2     0.60
1       0.50
0.8     0.40
	
Formula: A = V / (0.5)	
Volts	Amps
0.3     0.6
0.4     0.8
0.5     1
0.6     1.2
0.7     1.4
0.75    1.5
~~~

## TMC2100

These seem like either a meme that people fall for, or the best thing since sliced bread. Either way there's a lot of misinformation and conflicting reports out about them.

Max constant current is 1.25A, though they can jump up to 2.5A momentarily. The current/voltage formula is:

~~~
Formula: V = A / (1.77 / 2.5)		
Amps	Volts
0.5     0.71
0.55    0.78
0.75    1.06
1       1.41
1.25    1.77
		
Formula: A = V * (1.77 / 2.5)		
Volts	Amps
0.65    0.4602
0.77    0.54516
1       0.708
1.25    0.885
1.5     1.062
1.75    1.239
~~~

TMCs have two operating modes: **stealthChop** which is low torque and low noise, and **spreadCycle** which is high torque and a little noisier. Only spreadCycle is useful for 3D printers. One guy said his TMCs with spreadCycle configured resulted in louder operation than his old DRVs.

spreadCycle is entered by soldering two solder jumpers on the PCB, connecting CFG1 to ground. Some Chinese clone TMCs have this either mislabeled so you short out the chip, or don't have the IC's CFG1 actually exposed so you can never enter spreadCycle mode. Clones seem like a bad idea.

TMCs get up to 50C at 0.55A and will reach their 150C thermal shutoff at 1A, so require through-board heatpads attached to the bottom of the IC, large heatsinks, and active cooling (fans). I would build them into a tunnel housing with two quiet fans, one blowing air in and one blowing air out, like this:

~~~
.--------------------------------------------.
[>>]    h h      h h      h h      h h    [>>]
[>>]    h h      h h      h h      h h    [>>]
[>>]  TMC2100  TMC2100  TMC2100  TMC2100  [>>]
[>>]   |   |    |   |    |   |    |   |   [>>]
'--------------------------------------------'
~~~

Some cheap Chinese TMCs have no through-pad on the bottom, so cooling is much less effective. The white PCBs seem to be the good ones but this will probably vary per manufacturer. If you can't see what's under the heatsink, do not buy. Again clones seem like a bad idea.

TMCs apparently suffer the same high-pitched whine as DRVs due to the supply voltage difference. I don't know if the TL-Smoother circuit fixes this or not.

It's said that 1/256 microstepping results in less torque, however Tom has an explanation I don't understand for why they result in more effective torque:

* https://www.youtube.com/watch?v=g6Bxoqr8QlY
* https://www.youtube.com/watch?v=mYuZqx8xwTg

Considering all the unknowns, the fact they can only drive 1.25A, and the fact they cost $20 each (the same as an entire set of DRVs) I don't think TMCs are good value or suitable for 3D printers, or at least not worth the cost risk.

## References

* http://reprap.org/wiki/Stepper_motor_driver
* http://reprap.org/wiki/StepStick
* http://reprap.org/wiki/DRV8825
* http://reprap.org/wiki/TMC2100
* http://reprap.org/wiki/A4988_vs_DRV8825_Chinese_Stepper_Driver_Boards
* https://www.facebook.com/groups/1711323699127948/permalink/1881251935468456/ - Tom Keidar TMC findings on D-Bot Facebook Group