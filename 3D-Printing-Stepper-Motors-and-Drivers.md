# Stepper Motors

Learn how stepper motors work:

* https://www.youtube.com/watch?v=eyqwLiowZiU
* https://www.youtube.com/watch?v=bkqoKWP4Oy4

Modern 3D printers usually use NEMA17 motors which are 1.7" (43.2mm) square across the face. There are larger sizes like NEMA23 and NEMA34 which are common on CNCs. There are smaller sizes like NEMA14 and NEMA11 too. The first RepRap 3D printers used NEMA14s but the most powerful ones (40Ncm) were right on the limit of what they could do well.

Look up your motor's part number and pay attention to the **Step Angle**, **Holding Torque**, **Rated Current**, and **Voltage**.

3D printers need at least 35 Ncm holding torque. Generally the longer the motor the more torque it has, but not always, there are some "pancake steppers" specifically designed to be high-torque in a small light package.

You can gear up a motor, either with metal gears or printed gears, to increase the torque at the cost of decreasing speed. For example, a 3:1 gearset triples torque but results in a third of the speed.

Ideally you want the highest torque for the lowest current within the driver's capabilities. A 50Ncm 1.5A motor is a better choice than a 50Ncm 3A motor, none of the common drivers can even supply 3A.

Some people think it's better to pick a very powerful motor and under-drive it, to give a wild example pick a 100Ncm 2A motor and run it at 1A. I don't know if torque-to-current scales linearly.

Not every motor vendor publishes in Ncm so check other stupid manufacturer measurements at a torque converter like: http://www.numberfactory.com/nf%20torque.htm

* 1 N-cm = 0.1019716 kg-cm
    * 40 Ncm = 4.08 kg-cm
* 1 N-cm = 1.41612 oz-in
    * 40 Ncm = 56.64 oz-in

I find my extruder needs more current (1A to 1.2A) than the XYZ motion motors (0.75A) on my 1.3A 36Ncm motors.

Use the Step Angle to work out motor steps for firmware with: http://www.prusaprinters.org/calculator/

Also note there's really no point going above 1/32 microstepping with an ATmega2560, it can only supply that many steps reliably at 100mm/sec. You need at least that to bridge.

* http://reprap.org/wiki/Step_rates

~~~
TODO: Write my own Step Rates page, or maybe just correct RRW
~~~

## How to Tune Stepper Drivers

Turn power off, unplug the stepper motor cables, turn power back on and tune the stepper drivers.

When done, turn power off, plug in the stepper motor cables, turn power back on and test motor movement.

Don't tune stepper drivers with the motors plugged in, if you accidentally set current too high you can fry the motor or the stepper.

Don't plug or unplug stepper motors with the power on.

Measure DC voltage between the stepper trimpot and 12V ground. The ground at the 12V supply to the control board is fine to use.

Look up the correct current for your motor part number. If you have cheap Chinese motors with no part number, assume they have a max of 1.25A to be safe.

Look up the proper formula for your stepper drivers below, and find the voltage which corresponds with the current you want to set.

Pro tip: Get slip-on alligator clips for your multimeter. Clamp ground to a 12V ground wire and clamp positive to your screwdriver. This way you'll measure the voltage as you adjust and don't need three hands.

## References

* http://reprap.org/wiki/Stepper_motor
* http://reprap.org/wiki/NEMA_17_Stepper_motor

## Where to Buy in Australia

* [LearCNC](http://stores.ebay.com.au/learcnc)
    * NEMA17 - 67Ncm 1.5A (seems best, double check supply voltage, probably 4.8)
* [Stepper Online](http://stores.ebay.com.au/au-stepperonline)
    * NEMA17 - 45Ncm 2.0A 2.2V, 59Ncm 2.0A 2.8V, 65Ncm 2.1A 3.36V
    * NEMA14 - 40Ncm 1.5A 4.2V
    * All other sizes NEMA8 thru NEMA34
    * Pay attention, they sell a lot of motors with low current but high voltage (10V) demands

## Motors I Own

TEVO Tarantula ships with TEVO-branded `17HD40005-C5.18`.

The [TEVO Black Widow Community Guide](http://bit.ly/2k1dBoZ) says:

> TEVO has officially confirmed that these are an OEM version of the previously shipped `Busheng 17HD40005-22B`.

| Manufacturer | Part No       | Step Angle | Holding Torque | Current | Voltage | Weight
|---           |---            |---         |---             |---      |---      |---
| Busheng      | 17HD40005-22B | 1.8°       | 36Ncm          | 1.3A    | 2V      | 280g

* <http://www.haoyuelectronics.com/Attachment/17HD40005-22B/>
* <http://www.hotmcu.com/reprap-40mm-stepper-motor-p-214.html>

Aus3D sells Casun `42SHD0217-24B`.

The Casun website says 45Ncm but is unclear on other details. The datasheet on Aus3D says 50Ncm.

| Manufacturer | Part No       | Step Angle | Holding Torque | Current | Voltage | Weight
|---           |---            |---         |---             |---      |---      |---
| Casun        | 42SHD0217-24B | 1.8°       | 50Ncm          | 1.5A    | 3.75V   | 240g

* http://www.casunmotor.com/nema-17-stepper-motor
* http://aus3d.com.au/image/cache/catalog/products/stepper/40mmdatasheet-800x800.jpg

# Stepper Motor Drivers

I don't think there's any point going below 1/16 stepping with an 8-bit controller, the little MCU step rate is unable to keep up with very high speeds. I don't really see the advantage of 1/128 stepping when 1/256 interpolation exists. This essentially limits choices to A4988 or TMC2100.

| Manufacturer      | Chip    | Max Microstep | Max Current | Datasheet
|---                |---      |---            |---          |---
| Allegro           | A4988   | 1/16          | 2A          | [PDF](http://www.allegromicro.com/~/media/Files/Datasheets/A4988-Datasheet.ashx?la=en)
| Texas Instruments | DRV8825 | 1/32          | 2.2A        | [PDF](www.ti.com/lit/ds/symlink/drv8825.pdf)
| Allegro           | A5984   | 1/32          | 2A          | [PDF](www.allegromicro.com/~/media/Files/Datasheets/A5984-Datasheet.ashx?la=en)
| Sanyo             | LV8729  | 1/128         | 1.3A        | [Alldatasheet](http://www.alldatasheet.com/view.jsp?Searchword=LV8729)
| Sanyo             | THB6128 | 1/128         | 2.2A        | [Datasheet-PDF](http://www.datasheet-pdf.com/PDF/THB6128-Datasheet-ETC-817135)
| Shenzhenshi Yongfukang | HR4988  | 1/128    | 2A          | [PDF](http://www.szczkjgs.com/UploadFiles/fujian/3721/HR4988.pdf)
| Trinamic          | TMC2100 | 1/16 (16x)    | 1.2A        | [PDF](https://www.trinamic.com/fileadmin/assets/Products/ICs_Documents/TMC2100_datasheet.pdf)

## Allegro A4988

* 1/16 stepping
* 2A constant current max
* Most common so cheap and plentiful, a few dollars for a set of 5
* Check the sense resistor on clones, sometimes it is not 0.1R

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

## Texas Instruments DRV8825

* 1/32 stepping but can be set back to 1/16
* Much stronger than A4988 to move the carriage against
* Definitely the highest stepping you'd want to use with an 8-bit controller
* 2.2A constant max, 2.5A burst

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

They get a high-pitched whine, apparently due to the supply voltage (12V) being larger than the motor voltage (typically 2V to 2.8V). Some people say to use 4.2V motors and this goes away. Some people say to use higher motor voltage (24V) and this goes away.

There is a circuit which can get rid of this, with ready-made PCBs sold on Aliexpress as "TL-Smoother". The circuit is explained at:

* http://www.engineerination.com/2015/02/drv8825-missing-steps.html

This page also discusses noise:

* http://ebldc.com/?p=187

Some people say reducing current can also prevent the noise. For boards with digipots to adjust motor current, you could set the current high when printing, and low enough to hold the Z axis up when not printing, which would at least limit the noise. G-code to do this is in the format:

~~~
M907 X1.0 Y1.0 Z1.0 E1.5
~~~

* http://smoothieware.org/supported-g-codes

Apparently using a SilentStepStick Protector may help? See:

* http://forums.reprap.org/read.php?13,666367
* http://www.watterott.com/en/SilentStepStick-Protector

More research required on decay mode:

* https://www.youtube.com/watch?v=Wf8rN3bV8XM

## Sanyo LV8729

* Constant current advertised as either 1.3A or 1.5A.
* Peak current 1.8A
* 1/128 stepping, 32-bit board required

Not much info out there on these. Supposed to be quiet.

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

## Sanyo THB6128 (aka SD6128)

* 2.2A constant current
* Cooling unknown, needs at least big heatsinks
* 1/128 stepping, 32-bit board required
* `A = (V / 5) / R`

Sold in StepStick form factor as the [Panucatt SD6128](https://www.panucatt.com/product_p/sd6128.htm) or [RAPS128](http://reprap.org/wiki/RAPS128). Seems like a good idea.

## Shenzhenshi Yongfukang (Heroic) HR4988

* 2A constant current
* Apparently no cooling issues even at max current
* 1/128 stepping, 32-bit board required
* Use the same formula as A4988, they apparently come with 0.1R sense resistors

Cheap Chinese steppers available on Aliexpress, $25 for a set of 5. Seems too good to be true.

## Trinamic TMC2100

* 0.5A max constant current (no cooling)
* 1.25A max constant current (active cooling)
* 2.5A peak current
* 1/16 stepping, but the chip interpolates 16x in hardware, so the motor sees 1/256 stepping
* Best option for 8-bit boards, probably for 32-bit boards too
* Silent operation
* Be sure to enter into the proper mode for 3D printers, see below
* Don't buy cheap clones, they go about $20ea for good ones

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

TMCs have two operating modes: **stealthChop** which is low torque and low noise, and **spreadCycle** which is high torque and a little noisier. Only spreadCycle is useful for 3D printers. One guy said his TMCs with spreadCycle configured resulted in louder operation than his old DRVs, but most people say they are very quiet.

spreadCycle is entered by soldering two solder jumpers on the PCB, connecting CFG1 to ground. Some Chinese clone TMCs have this either mislabeled so you short out the chip and fry it, or don't have the IC's CFG1 actually exposed so you can never enter spreadCycle mode. Clones seem like a bad idea.

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

TMCs can apparently suffer the same high-pitched whine as DRVs due to the supply voltage difference. I don't know if the TL-Smoother circuit fixes this or not.

It's said that 1/256 microstepping results in less torque, however Tom has an explanation I don't understand for why they actually result in more effective torque:

* https://www.youtube.com/watch?v=g6Bxoqr8QlY
* https://www.youtube.com/watch?v=mYuZqx8xwTg

Previously I wasn't sure if TMCs were good or a meme, but after researching more and speaking to people who own them and get them properly into spreadCycle mode with proper cooling, they seem the best option all round.

## References

* http://reprap.org/wiki/Stepper_motor_driver
* http://reprap.org/wiki/StepStick
* http://reprap.org/wiki/DRV8825
* http://reprap.org/wiki/TMC2100
* http://reprap.org/wiki/A4988_vs_DRV8825_Chinese_Stepper_Driver_Boards
* https://www.facebook.com/groups/1711323699127948/permalink/1881251935468456/ - Tom Keidar TMC findings on D-Bot Facebook Group