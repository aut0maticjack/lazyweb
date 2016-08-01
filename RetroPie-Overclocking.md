## Aim

Improve and possibly combine these:

* https://github.com/RetroPie/RetroPie-Setup/wiki/Overclocking
* https://github.com/RetroPie/RetroPie-Setup/wiki/Optimization%20for%20Nintendo%2064
* https://github.com/RetroPie/RetroPie-Setup/wiki/Speed-Issues

## Status

Work in Progress

## Defaults

| config.txt   | Pi 1 B  | Pi 2  | Pi 3  | Zero  |
| -------------|---------|-------|-------|-------|
| `arm_freq`   | 700     | 900   | 1200  | 1000  |
| `core_freq`  | 250     | 250   | 400   | 400   |
| `gpu_freq`   | ?       | ?     | 300   | 300   |
| `sdram_freq` | 400     | 450   | 450   | 450   |

## Expected Useful Overclocks

~~~
core_freq=500
gpu_freq=500
sdram_freq=500
~~~

## Warranty Voids

~~~
force_turbo=1
# disables frequency scaling so cores always run at max speed
# enables h264 isp and v3d individual overclock (also requires avoid_pwm_pll=1 i think?)

temp_limit=
# anything greater than 85

over_voltage=
# anything greater than 6
# minimum setting -16 = 0.8 V
# default setting   0 = 1.2 V
# maximum setting   8 = 1.4 V

current_limit_override=0x5A000020
# disables over-current protection, not recommended
# http://www.raspberrypi.org/phpBB3/viewtopic.php?f=29&t=6201&start=325#p170793
~~~

## Overclock Stability Test

There's a script of `yes` and `dd` loops at http://elinux.org/RPiconfig#Overclocking but I'm not sure that's so useful, it just causes bash to spin in simple task switching instructions and doesn't test the GPU at all.

I'm going to calculate prime numbers on all cores to max the CPU while running Conker's Bad Fur Day on N64 to max the GPU.

~~~
sysbench --num-threads=$(nproc --all) --test=cpu --cpu-max-prime=10000000 run
~~~

## Monitoring

* `htop` - process CPU usage
* `vcgencmd measure_temp` - temperature
* `for src in arm core h264 isp v3d pixel; do echo -e "$src:\t$(vcgencmd measure_clock $src)"; done` - current speeds
* `sudo vcdbg reloc | awk -F '[ ,]*' '/^\[/ {sum += $12} END { print sum / 1024 / 1024 }'` - VRAM usage in MiB

## Games Which Benefit From Overclocks

* NARC (arcade) `narc.zip` added 0.34b7 [emma](http://www.progettoemma.net/index.php?gioco=narc&lang=en)
* Ultimate MK3 (arcade) `umk3.zip` added 0.37b5 [emma](http://www.progettoemma.net/index.php?gioco=umk3&lang=en)
* NBA Jam TE (arcade) `nbajamte.zip` added 0.36r2 [emma](http://www.progettoemma.net/index.php?gioco=nbajamte&lang=en)
* Super Mario 64 (N64)

## Other Messy Notes

* dankcushions reckons N64 games are mostly GPU-bound not CPU-bound, so there's no point to overclocking ARM
* Few people seem to be able to get a Pi 3 ARM to 1.4GHz
* Nintendofreak18's wiki at http://wiki.freakybigfoot.com/index.php/Raspberry_Pi_3_Overclocking