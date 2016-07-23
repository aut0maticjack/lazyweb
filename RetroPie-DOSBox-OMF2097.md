This is a fairly complete guide on installing the excellent [One Must Fall: 2097](https://en.wikipedia.org/wiki/One_Must_Fall:_2097) in RetroPie's DOSBox so you can play it with a gamepad.

This assumes knowledge of how to SSH into your Pi or use the commandline, how to edit and save config files in Linux, and how to use the keymapper in DOSBox.

You need a keyboard and mouse connected for the initial setup, but not to play once it's properly setup.

I started with the RetroPie 4.0.0 beta2 image.

### Install DOSBox

Run the setup script:

~~~
cd ~/RetroPie-Setup
sudo ./retropie_setup.sh
~~~

Manage Optional packages, Install `dosbox` package.

### Configure DOSBox

I set the joystick type to FCS Thrustmaster so it recognises my axis-based D-Pad as joystick input. I don't know if this is required in DOSBox-SVN on the Pi, but I have to do this on my desktop DOSBox-0.74 setup so I did it here too:

~~~
/opt/retropie/configs/pc/dosbox-SVN.conf

joysticktype=fcs
~~~

Launch the DOSBox keymapper to bind a keyboard keypress to a joystick button by running:

~~~
/opt/retropie/emulators/dosbox/bin/dosbox -startmapper
~~~

I configured like this:

* Enter key = B button
* Right Shift key = Y button
* Esc key = Select button
* Arrow keys = D-Pad

Using a Logitech F710 resulted the following changes to the mapper file:

(I'm not sure which of these mapper file paths is right. I think I saved it in `~/.dosbox/` and it was copied into `/opt/` automatically)

~~~
~/.dosbox/mapper-SVN.map
/opt/retropie/configs/pc/mapper-SVN.map

key_esc "stick_0 button 6" "key 27" 
key_enter "stick_0 button 0" "key 13" 
key_rshift "stick_0 button 2" "key 303" 
key_up "stick_0 hat 0 1" "key 273" 
key_left "stick_0 hat 0 8" "key 276" 
key_down "stick_0 hat 0 4" "key 274" 
key_right "stick_0 hat 0 2" "key 275" 
~~~

I also removed the joystick mappings later in this file which were added automatically. Any entry which starts with `j` just remove the configured parameter from it so you have an empty list like this:

~~~
jbutton_0_0
jbutton_0_1
jaxis_0_1-
jaxis_0_1+
jaxis_0_0-
jaxis_0_0+
jbutton_0_2
jbutton_0_3
jbutton_1_0 
jbutton_1_1 
jaxis_0_2-
jaxis_0_2+
jaxis_0_3-
jaxis_0_3+
jaxis_1_0- 
jaxis_1_0+ 
jaxis_1_1- 
jaxis_1_1+ 
jbutton_0_4
jbutton_0_5
jhat_0_0_0
jhat_0_0_3
jhat_0_0_2
jhat_0_0_1
~~~

### Install OMF

Put OMF in the `/home/pi/RetroPie/roms/pc/OMF` directory

I copied an existing install from my PC so I had already run `SETUP.EXE` and configured the soundcard. If you haven't done this, connect a USB keyboard and do so.

On a Pi 1 overclocked to 900/450/450/2, the highest sound setting resulted in crackling, I had to configure a lower performance sound setting in the setup program. I haven't tried a Pi 2 or Pi 3 yet.

### Create Launcher

~~~
cd ~/RetroPie/roms/pc
cp "+Start DOSBox.sh" "One Must Fall 2079.sh"
~~~

In that new file, setup the parameters to launch and quit automatically:

~~~
    params=(-c "@MOUNT C /home/pi/RetroPie/roms/pc" -c "@C:" -c "@CD OMF" -c "@FILE0001.EXE" -c "@EXIT")
~~~

Restart EmulationStation and you're done!

### References

* http://dosonthepi.blogspot.com/2015/01/run-dos-games-in-retropie_15.html
* http://dosonthepi.blogspot.com/2015/01/configure-game-controllers-in-dosbox_29.html
* http://www.dosbox.com/DOSBoxManual.html#Joystick