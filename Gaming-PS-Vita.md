A page about using a hacked PlayStation Vita as a replacement for a hacked PSP.

Mostly things nobody tells you or which are nontrivial to figure out yourself.

## Assumed Knowledge

* Firmware versions which work or are hackable
* How to install Henkaku
* How to install Enso if desired
* How to install Adrenaline
* I'm not really interested in Vita piracy but you can look up NoNpDRM or MaiDump or Vitamin

## Charging the Vita

* Via USB, Vita will only charge when it is off (not on, not sleeping)
* With the official AC adapter, Vita also charges when on and in use

## CPU Speed

* Vita runs up to 333 MHz with wifi on, and 444 MHz with wifi off, so turn wifi off I guess
* There is overclocking called [LOLIcon](https://github.com/dots-tb/LOLIcon/releases) but there's forum posts saying people have got their Vita into an unuseable or unbootable state with it, so I've never bothered

## File Transfers

* VitaShell FTP is slow (like 30 minutes to transfer 1GiB)
* If you leave the FTP server idle, it times out. To get around this, exit from VitaShell and swipe it away, then go back into VitaShell, start the FTP server again.
* You can sync files via the official app or [qcma](https://codestation.github.io/qcma/) on Mac/Lin but I haven't tried this yet
* "Refresh the LiveArea" is done from VitaShell, while at the list of filesytems press Triangle

## Adrenaline

* The PSP game location is `ux0:/pspemu/PSP/GAME/`
    * Example: `ux0:/pspemu/PSP/GAME/Wipeout/EBOOT.pbp`
* The PSP ISO/CSO location is `ux0:/pspemu/ISO`
    * Example: `ux0:/pspemu/ISO/Tactics Ogre.iso`
* Don't make file names too long or Adrenaline will say **Corrupted Data**. I think you are actually supposed to use the gameid like `SLUS12345` or whatever.
* Use [Adrenaline Bubble Manager](https://github.com/ONElua/AdrenalineBubbleManager) to put PSP game shortcuts in the Vita Live Area so you don't have to launch Adrenaline to play

## Emulators

* Most native emulators are not as good as RetroArch. Get the latest from: https://buildbot.libretro.com/stable/
* SNES - Use RetroArch cores `snes9x2005` or `snes9x2010`, the most recent snes9x has performance problems for me
* OutRun - Use [Cannonball](https://github.com/rsn8887/cannonball/releases)

## Links

* Basic Howto
    * http://wololo.net/vita-cfw4dummies/
    * https://nblog.org/guides/nicoblogs-ps-vita-general-guide/
    * https://gbatemp.net/threads/guide-the-ultimate-noob-ps-vita-pstv-hacking-guide-check-here-first.403035/
* Henkaku
    * http://henkaku.xyz/
    * https://enso.henkaku.xyz/
* Software
    * VitaShell - https://github.com/TheOfficialFloW/VitaShell/releases
    * VitaTweaks - https://github.com/TheOfficialFloW/VitaTweaks
    * VitaIdent - https://github.com/joel16/VITAident/releases
    * Adrenaline - https://github.com/TheOfficialFloW/Adrenaline/releases
    * Adrenaline Bubble Manager - https://github.com/ONElua/AdrenalineBubbleManager/releases
* Games and Emulators
    * Cannonball - https://github.com/rsn8887/cannonball/releases
    * Chocolate Doom - https://github.com/fgsfdsfgs/chocolate-doom/releases

## Things I Don't Know Right Now

* SD2Vita - use a common MicroSD card instead of Sony's expensive memory card
* QCMA file transfers on Linux
* NoNpDRM - newest Vita piracy method - https://github.com/TheOfficialFloW/NoNpDrm
* MaiDump - older Vita piracy method - https://github.com/LioMajor/MaiDumpToolEN/
* Vitamin - older Vita piracy method
* https://www.reddit.com/r/VitaPiracy/