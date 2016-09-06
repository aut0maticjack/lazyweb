## Config File

The DOSBox config file is at `~/.dosbox/dosbox-SVN.conf`

## C Drive

I put my C drive in `~/RetroPie/roms/DOS` and then edit the launcher `RetroPie/roms/pc/+Start\ DOSBox.sh` to have the line:

~~~
    params=(-c "@MOUNT C /home/pi/RetroPie/roms/DOS" -c "@C:")
~~~

This keeps the PC menu in RetroPie tidy.

## Per-game Config

~~~
    params=(-conf "~/.dosbox/game.conf" -c "@MOUNT C /home/pi/RetroPie/roms/DOS" -c "@C:")
~~~

To have a custom key map, in that config file, set:

~~~
mapperfile=mapper-game.map
~~~

## Keymapper

Good ideas:

* mod3 = Select
* Shutdown = Start
* Cycles Down = L2
* Cycles Up = R2

Logitech F710:

~~~
mod_3 "stick_0 button 8" 
hand_shutdown "key 290 mod1" "stick_0 button 9 mod3" 
hand_cycledown "stick_0 button 6 mod3" "key 292 mod1" 
hand_cycleup "key 293 mod1" "stick_0 button 7 mod3" 
~~~

Should probably make a convention like:

* L2 = y
* R2 = n
* Select = Esc
* Start = Enter

## Aspect Ratio

To get games to display in the correct aspect ratio:

~~~
windowresolution=1024x768
output=overlay
aspect=true
~~~

Setting `output=opengl` does not harm performance and applies bilinear smoothing to make things look nicer, though it also renders a mouse cursor in the top left corner which is rather annoying.

Setting `windowresolution=1280x960` looks nicer but performance suffers. Maybe this is OK to use with less demanding games.

Setting `scaler=normal2x` doesn't seem to make any performance difference, unsure if it makes a graphical difference either.

## Performance

I always configure my DOSBox with a fixed cycles count like:

~~~
core=auto
cputype=auto
cycles=20000
cycleup=1000
cycledown=1000
~~~

Doom maxes out the CPU at 21000 cycles, which gives about 21fps, about the performance of a 486-66 according to the Doom Benchmark.

Performance depends on the game, OMF2097 performs well on its "Pentium" setting with only 10000 cycles. IIRC from using real hardware, that setting actually did require a Pentium or faster.

Probably worth playing with `cycles=max` with some games. In Doom this dropped 4fps. In OMF2097 it makes the game unplayably fast.

## Compiling from Source

The binaries RetroPie provides are compiled with the Pi 2 compiler flags, but recompiling on a Pi 3 uses different flags, which appears to give a boost in performance. I haven't benchmarked this.

## References

* https://www.reddit.com/r/RetroPie/comments/50q04s/getting_320x200_dos_games_to_display_correctly/
* https://www.complang.tuwien.ac.at/misc/doombench.html