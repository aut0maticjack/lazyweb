# G-Code

G-Code is the "language" our printers speak. Every instruction which results in a change or action on the printer is G-Code.

If you are old, you may have used an Apple II in school. These computers had a language called Logo which had a "turtle" that could move around and draw a line as it moved. You can see from the picture below, if you tell the turtle `forward 100 pixels` and `right 90 degrees` enough times, you will draw a square:

![Logo Turtle](https://theantiroom.files.wordpress.com/2011/04/logo_turtle.jpg)

3D printers and G-Code work the same way. Heat the nozzle to a certain temperature, move the nozzle around left/right/up, move the filament extruder forward at the correct rate, and your plastic part is created. It's just a more complex version of the turtle.

There is a giant list of all supported G-Code on the RepRapWiki, however that's a huge list and is not very gripping reading. It is a very good reference though, so bookmark it:

* http://reprap.org/wiki/G_code

Not every G-Code operates the same on every firmware, some do/don't implement some codes, or there may be slight differences in operation. Each printer firmware may document specific details of its supported G-Code better than the RepRap Wiki:

* http://marlinfw.org/meta/gcode/
* https://duet3d.com/wiki/G-code
* http://smoothieware.org/supported-g-codes

But this are still large lists. Where's the crash course? Inspired by the rather clickbait-titled [The 10 Most Common G-Code Commands for 3D Printing](https://www.simplify3d.com/support/articles/3d-printing-gcode-tutorial/) by S3D, this article is a list of useful G-Code you can have in the start/stop G-Code of your slicer or may realistically find useful to learn.

## Useful G-Code

### `;` - Comment

The `;` character doesn't do anything, it's considered a comment. The comment can be either on a line on its own, or after valid G-Code. For example, both of these are the same and the firmware will only see `G28`:

~~~
; perform home sequence
G28
~~~

~~~
G28 ; perform home sequence
~~~

### `G28` - Perform Home Sequence

`G28` tells your printer to perform the home sequence. 3D printers work on an "open loop" control system, meaning they find the home position (usually minimum or maximum travel) with the Home command, and then keep track of movement from that point.

The printer knows it's at position 0 because the switch activated. If it moves 100 right then 50 right, it knows it's at position 150. If it moves 100 left, it knows it's at position 50. If we come along and moves the motor manually with our hand (or more likely in real life, the motor skips steps) then the printer doesn't know about that, it still thinks it's at position 50. That's why we home.

There do exist "closed loop" systems where the motor knows how much it's moved and can feed that information back to the control board and firmware. These are usually called "servo motors" or "encoders". These are quite expensive so not common to see on hobby-level 3D printers, but there are a few projects out there to convert our cheap stepper motors into feedback-capable servo motors.

Read more on RRW:

* http://reprap.org/wiki/Motor_control_loop

You can also specify specific axes to home. For example, to home only the X and Y axis: `G28 X Y`

### `G29` - Perform Auto-Level Sequence

TODO. for all y'all fancy inductive probe or BLTouch or IR probe users

### `G1` - Move

### `G90` and `G91` - Set Positioning Mode

TODO. helpful to Z hop out of the way

### `G92` - Set Position

TODO.

### `M92` - Set axis steps per unit

TODO. useful when testing and tuning esteps

### `M104` and `M109` - Extruder Temperature Control

TODO. turn extruder off after print

### `M140` and `M190` - Bed Temperature Control

TODO. turn bed off after print

### `M106` and `M107` - Fan Control

TODO. see what fan speed/noise is like, turn fan off after print

### `M117` - Display Message

TODO. `M117 PC LOAD LETTER` for lulz

### `M119` - Get Endstop Status

TODO. useful when troubleshooting endstops

### `M201` to `M204` - Speed and Acceleration Control

### `M302` - Allow Cold Extrude

TODO. useful when tuning esteps

### `M303` - PID Autotune

TODO. see calibration page for firmware specifics

### `M500` to `M502` - EEPROM Commands

TODO. i don't use eeprom

## Useful Start G-Code

~~~
G28
G29 ; if you have a Z probe
~~~

If you have a simple printer or you prefer manual bed levelling, `G28` is all you need in your start G-Code. In fact, if you're willing to home before you start printing, you don't really even need that, but it's a good idea to keep it in. It doesn't take long.

If you have a bed probe, you could also add the probe sequence `G29`, however if you can't be bothered waiting for your printer to manually touch 9 or 16 or 25 points of the bed before each and every print, maybe it's easier if you just do the bed probe from the LCD screen or Pronterface or OctoPrint or however you do it. Unless your printer has a very unstable bed, a manual probe should last at least a few prints before needing to be done again.

## Useful End G-Code

~~~
M104 S0 ; hotend off
M140 S0 ; bed off
M107 ; fan off
G1 X0 F3600; move carriage out of the way
G1 Y200 F3600 ; present print for mendels
M84 ; motors off
~~~

### References

* http://reprap.org/wiki/G_code
* https://en.wikipedia.org/wiki/G-code
* https://www.simplify3d.com/support/articles/3d-printing-gcode-tutorial/
