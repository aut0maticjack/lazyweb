### tl;dr

Try this free Pi 2 Raspbian Wheezy image with x86 Wine preinstalled, it runs about the speed of a 300MHz PC, I don't think it supports Pi 3 as-is but I haven't tried:

* https://github.com/AlbrechtL/RPi-QEMU-x86-wine

----

### Background

Every now and then, someone pops up asking if they can play their favorite PC game on the Raspberry Pi. The answer is usually no, PC games are made for the x86 architecture but the Pi uses ARM architecture and the two are not compatible.

### DOSBox and Wine

DOSBox does exist and allows DOS PC games to work on the Raspberry Pi. [My own testing](https://www.complang.tuwien.ac.at/misc/doombench.html) has found the Pi 3 performs at roughly the speed of a 486 66MHz.

However, people often do not mean DOS games, they mean Windows games.

[Wine](https://www.winehq.org/) can be used to run Windows applications on x86 Linux but it is not a solution here either. Wine literally stands for **W**ine **I**s **N**ot an **E**mulator. Wine is an application call translation layer. The basic idea is that a Windows application says something like "*Hey Windows, draw the game window here*" and Wine translates that into "*Hey Linux Xorg, draw the game window here*". The actual application code is still x86 and executes natively, it's only the operating system parts like graphics/sound/input that are translated to Linux.

### Aim

One of the most commonly-requested games is Fallout 2, so this page explores possible ways to run 1990s 32-bit Windows games which use little or no 3D such as:

* [Mechwarrior 2: 31st Century Combat](https://en.wikipedia.org/wiki/MechWarrior_2:_31st_Century_Combat)    
  Dec 1995, Win95, 100 MHz CPU, 16 Mb RAM, Direct3D (DirectX 3) ([PCGW](http://pcgamingwiki.com/wiki/MechWarrior_2:_31st_Century_Combat))
* [Mechwarrior 2: Mercenaries](https://en.wikipedia.org/wiki/MechWarrior_2:_Mercenaries)  
  Sept 1996, Win95, 100 MHz CPU, 16 Mb RAM, Direct3D (DirectX 3) ([PCGW](http://pcgamingwiki.com/wiki/MechWarrior_2:_Mercenaries))
* [Diablo](https://en.wikipedia.org/wiki/Diablo_(video_game))  
  Dec 1996, Win95/NT, 60 MHz CPU, 8 MB RAM (16 MB for multiplayer), SVGA video card, DirectX 3 ([wiki](http://www.diablowiki.net/Diablo_I), [PCGW](http://pcgamingwiki.com/wiki/Diablo))
* [StarCraft](https://en.wikipedia.org/wiki/StarCraft_(video_game))  
  Mar 1998, Win95, 90 MHz CPU, 16 Mb RAM, SVGA video card, DirectDraw at 640x480 256 colors ([PCGW](http://pcgamingwiki.com/wiki/StarCraft))
* [Fallout 2](https://en.wikipedia.org/wiki/Fallout_2)  
  Sept 1998, Win95, 90 MHz CPU, 16Mb RAM; DirectX 3.0a, 1 Mb VESA SVGA video card, Sound Blaster sound card ([wiki](http://fallout.wikia.com/wiki/Fallout_2), [PCGW](http://pcgamingwiki.com/wiki/Fallout_2)) 

This page is *not* about later 3D accelerated games like [Half-Life](https://en.wikipedia.org/wiki/Half-Life_(video_game)) (1997) or [Unreal Tournament](https://en.wikipedia.org/wiki/Unreal_Tournament) (1999) or [Deus Ex](https://en.wikipedia.org/wiki/Deus_Ex) (2000) or Fallout 3 or Portal or Crysis or World of Warcraft or Warcraft 3 or Counter-Strike or DotA or Team Fortress or anything like that.

### Windows 9x in DOSBox

I've always heard about this but I never really looked into it. A Google search returns these guides:

* [Running Windows 95 in DOSBox - A comprehensive how to guide](http://dosbox95.darktraveler.com/) (also has Win98)
* [Guide: installing Windows 95 on DOSBox by dada](https://docs.google.com/document/d/1hvgFvAYjPG93h-Avun3sprvZX2GfkRhl4YJBT15FTx0/edit)
* [A Complete Guide to Install Windows 95 on DOSBox by D.Sync](http://dsync.blogspot.com/2014/03/a-complete-guide-to-install-windows-95.html)

This would probably work well on a powerful desktop PC, but considering DOSBox performance on Pi 3 is about equal with a 486 66MHz, this probably would not work very well on Raspberry Pi.

### ExaGear Desktop

[ExaGear Desktop](https://eltechs.com/product/exagear-desktop/) is a software product made by Russian company Eltechs. It claims to be able to run x86 Windows applications on Raspberry Pi ARM. A license costs US$16.45 for Pi Zero and US$27.45 for Pi 2 and Pi 3 (and Pi 3 support is marked as beta).

ExaGear sounds very intriguing, however most peoples' introduction to it is some blog-like post submitted to [r/raspberry_pi](https://www.reddit.com/r/raspberry_pi/) which ends up actually being an advertisement written by an Eltechs employee. There is at least one Eltechs employee who claims to be the CEO. There may not be greater than one employee. Despite several threads where I've asked ExaGear to upload videos demonstrating some common 90s Windows games running and them saying they would, there have been no such things forthcoming. This sort of deceptive marketing and lack of proof makes me really question whether this product can do what it claims.

There are some things we can learn about ExaGear from the various things said by and around them:

* The license is tied to a single Pi, it is not transferable
* There is no trial version
* There is no refund
* There is no 3D acceleration
* Performance seems a little slower than a 500MHz x86 PC
* There is an open source repository at https://github.com/Eltechs/wine with exagear branches

The MagPi looked at ExaGear in their [Issue 35 from July 2015](https://www.raspberrypi.org/magpi/issues/35/) on Page 58. This explains much more about the technology, it's using a QEMU emulation layer to run a Debian or Ubuntu container or virtual machine image which can have Wine installed in it. They described that getting x86 Linux working was easy, but getting 32-bit x86 Windows software running was very hard and that "only very old" software could be used. This could be due to the old Wine 1.6.2 version included and lack of Wine compatibility or simply because they expected it to run more modern 3D Windows apps than I would be interested in. Their conclusion is:

> *In all, we found ExaGear Desktop provided no practical use for Windows software, but was fantastic for running Linux x86 programs.*

ODROID Magazine looked into ExaGear for their [February 2015 issue](http://forum.odroid.com/viewtopic.php?f=74&t=5085#p70712). This is even more detailed, saying this is a virtual machine, it can do some software Mesa emulation of basic OpenGL 3D but not much (eg: not enough to even run the Steam client), and talks more about usage and launching it. There is a screenshot of [Total Annihilation](https://en.wikipedia.org/wiki/Total_Annihilation) (Sept 1997, Win95, 100 MHz CPU, 16Mb RAM, [PCGW](http://pcgamingwiki.com/wiki/Total_Annihilation)) running on an ODroid U3 which is right on target for the sort of games I'm looking at here.

To be honest I expect ExaGear Desktop on Pi 3 would run all the Win9x games I listed above just fine. I don't know why ExaGear are so evasive about this. If they just put up some good videos showing it running things like Diablo and StarCraft the sales would probably come rolling in. Oh well, that's their silly mistake to make.

There are also ExaGear versions for Android:

* https://play.google.com/store/apps/details?id=com.eltechs.erpg
* https://play.google.com/store/apps/details?id=com.eltechs.es

There are various YouTube videos demonstrating these working pretty well on fast devices (I guess about 2013 onwards or Tegra 4 onwards) but this page isn't about Android.

### Patched QEMU and Wine

Whilst reading these Raspberry Pi Forum threads about all this:

* [Wine on Raspberry Pi](https://www.raspberrypi.org/forums/viewtopic.php?f=41&t=12727)
* [Running x86 apps on ARM](https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=111858)

I came across this image of a pre-made Rasbian Wheezy with Wine 1.5.2 and a QEMU 1.4.0 patched to allow running of x86 binaries on ARM:

* https://github.com/AlbrechtL/RPi-QEMU-x86-wine

The QEMU source is up at:

* https://github.com/AlbrechtL/qemu

The patches needed to get this working are on the WineHQ forums at:

* https://forum.winehq.org/viewtopic.php?f=8&t=17701&start=25#p84325

This must be what ExaGear does. Performance is apparently about equal with a 300MHz x86 PC. It doesn't seem the creator has applied any of these patches to Raspbian Jessie, and it's not clear if the Pi 2 image supplied works on a Pi 3 (or ever could).

### Future Ideas

* Try update AlbrechtL's Wheezy image for the Pi 3
* Try get QEMU with NPTL patch working on Jessie on Pi 3
* Try get Wine with NPTL and epoll patches working on Jessie on Pi 3
* Try compile Eltechs' ExaGear source on Jessie on Pi 3
* Try use the Raspberry Pi 2 Cortex A7 compile flags from RetroPie:  
  `-O3 -mcpu=cortex-a7 -mfpu=neon-vfpv4 -mfloat-abi=hard -funsafe-math-optimizations`
* Try use the Raspberry Pi 3 Cortex A53 compile flags from RetroPie:  
  `-O3 -march=armv8-a+crc -mtune=cortex-a53 -mfpu=neon-fp-armv8 -mfloat-abi=hard -funsafe-math-optimizations`