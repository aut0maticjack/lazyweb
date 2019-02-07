A page about using a hacked PlayStation Vita as a replacement for a hacked PSP.

Mostly things nobody tells you or which are nontrivial to figure out yourself.

## Assumed Knowledge

* Firmware versions which work or are hackable
* How to install Henkaku
* How to install Enso if desired
* How to install Adrenaline
* I'm not really interested in Vita piracy but you can look up NoNpDRM or MaiDump or Vitamin for these

## Charging the Vita

* Via USB, Vita will only charge when it is off (not on, not sleeping)
* With the official AC adapter, Vita also charges when on and in use

## File Transfers

* VitaShell FTP is slow (like 30 minutes to transfer 1GiB)
* If you leave the FTP server idle, it times out. To get around this, exit from VitaShell and swipe it away, then go back into VitaShell, start the FTP server again.
* You can sync files via the official app or [qcma](https://codestation.github.io/qcma/) on Mac/Lin but I haven't tried this yet

## Adrenaline

* The PSP game location is `ux0:/pspemu/PSP/GAME/`
    * Example: `ux0:/pspemu/PSP/GAME/Wipeout/EBOOT.pbp`
* The PSP ISO/CSO location is `ux0:/pspemu/ISO`
    * Example: `ux0:/pspemu/PSP/GAME/Tactics Ogre.iso`
* Don't make file names too long or Adrenaline will say **Corrupted Data**
* Use [Adrenaline Bubble Manager](https://github.com/ONElua/AdrenalineBubbleManager) to put PSP game shortcuts in the Vita Live Area so you don't have to launch Adrenaline to play

## Emulators

* Most native emulators are not as good as RetroArch. Get the latest from: https://buildbot.libretro.com/stable/
* SNES - Use RetroArch cores `snes9x2005` or `snes9x2010`, the most recent snes9x has performance problems for me
* OutRun - Use [Cannonball](https://github.com/rsn8887/cannonball/releases)
