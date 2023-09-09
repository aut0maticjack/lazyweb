# Classic / Compact Macintosh Notes

This is a crash course in Compact Macintosh (Motorola 68000 CPU family) for people who never had anything to do with them.

I'm writing from the perspective of someone who grew up with DOS and Windows, though now I use Linux and have for almost 20 years.

Warning: I mostly ignored these systems until 2023 and have almost no idea what I'm talking about, so it's very likely I've got something wrong. Comments and corrections are very welcome. Find me at <https://fosstodon.org/@suprjami>

## Hardware

* <https://en.wikipedia.org/wiki/Compact_Macintosh>
* <https://en.wikipedia.org/wiki/Macintosh_II_family>
* <https://www.lowendmac.com/early-macs.html>

Read the history of these from 128K to Mac II, but focus will be on the **Mac Plus** and **Mac II** because those are what Mini vMac emulates by default.

* Mac Plus: 8MHz 68000, 1 MiB to 4 MiB RAM, 9" 512 x 384 black-and-white CRT, System 3.0 to 7.5.5
* Mac II: 16 MHz 68020, 1 MiB to 8 MiB RAM, 13" or 14" 640x480 256-color CRT, System 4.1 to 7.5.5
    * In real life, you can use a "32-bit clean" ROM from a different model (IIci?) to get up to 128M RAM - imagine that in 1990!

## Software - OS

* <https://en.wikipedia.org/wiki/Classic_Mac_OS>

### Operating System 1.0 to 6.0.x

The operating system from 1.0 to 6.0 was called "System Software" and typically was not installed on a hard drive until maybe 6.0.x. The original Mac 128K and 512K didn't even have a hard drive in their original form (but you could get aftermarket ones). Instead, you'd boot the system from the OS floppy and then eject it, inserting another floppy to run an application.

It might seem weird to eject the operating system disk, but the "ROM" of the Mac was not a simple "BIOS" like we think of in a DOS computer. Depending on model, the ROM held a subset of the operating system API like GUI window drawing routines. This would be like Microsoft releasing their own computer and putting half of the Windows API in the BIOS.

Another way programs ran was to boot from their own floppy, which had a subset of the System Software on it. This is probably similar to a DOS boot disk which was prepared with `FORMAT /S A:` with its own `CONFIG.SYS` and `AUTOEXEC.BAT` and a game or application which ran off that bootdisk.

### Operating System 7.0 / 7.1 / 7.5

* <https://en.wikipedia.org/wiki/System_7>

These operating system versions were still called "System Software" and were the last version with support for the original 68k hardware with 7.5.5.

As of 7.6 the name changed to "Mac OS" and required newer "[32-bit clean](https://en.wikipedia.org/wiki/32-bit_clean)" 68k systems to run.

As far as I can tell, System 7 was always (or almost) installed on hard drives.

This brought several architectural changes to the OS such as virtual memory, "System Extensions" which are like drivers so you could install support for a specific thing, aliases which are like symlinks on Linux, drag-and-drop of documents onto applications.

The install/upgrade paths for these are:

* 7.0: Install from System 7.0.1 floppies, apply System 7.0.1 Tune-Up 1.1.1
* 7.1: Install from System 7.1 floppies, apply System 7.1 System Update 3.0
* 7.5: Install from System 7.1 floppies, apply System 7.5.3 upgrade, apply System 7.5.5 upgrade

### Which to Choose?

People seem to have very strong opinions about which is the best OS for which Classic Mac:

* [Selecting your System Software for your 68k Macintosh - Savage Taylor, 2015](https://www.savagetaylor.com/2015/11/17/setting-up-your-vintage-classic-68k-macintosh-selecting-your-system-software/)
* [Which System Software Is Best for My Vintage Mac? - Tyler Sable, 2014](https://lowendmac.com/2014/which-system-software-is-best-for-my-vintage-mac/)
* [Why Do I Prefer System 7.5.5? - Scott Barber, 1999](https://lowendmac.com/1998/why-do-i-prefer-system-7-5-5/)
* [What’s the Best System Version for My Mac? - Daniel Knight, 1998](https://lowendmac.com/1998/whats-the-best-mac-system-version/)

My interest is solely in emulators which let us run at unrealistically fast speeds with hardware combinations that didn't even exist in real life. System 7.0 and 7.1 don't support a lot of useful software. I don't really see a compelling reason to use anything except System 7.5.5 in an emulated system.

### Where to Get?

* [WinWorld: System Software 0-6](https://winworldpc.com/product/mac-os-0-6/system-6x)
* [WinWorld: Mac OS 7](https://winworldpc.com/product/mac-os-7)
* [Internet Archive mirror of Apple](https://ia803407.us.archive.org/view_archive.php?archive=/33/items/download.info.apple.com.2012.11/download.info.apple.com.2012.11.zip)
* <https://macintoshgarden.org/apps/system-7-floppy-sets>

You'll also need a ROM image, those are around the place:

* <https://archive.org/download/mac_rom_archive_-_as_of_8-19-2011>
* <https://www.macintoshrepository.org/7038-all-macintosh-roms-68k-ppc->
* <http://hampa.ch/pub/software/ROM/Macintosh%2068K/>

### How to Use?

The OS gives you a tutorial on first boot, do that to learn some basic usage and keyboard shortcuts.

To "eject" a disk, drag it to the trash can.

The "Command" key **⌘** is **Alt** in emulators.

The desktop is shared amongst all mounted disks, so if you have multiple disks mounted it's difficult to tell which disk owns which desktop folder. Don't store stuff on the desktop if this is confusing.

## Emulators

There are two main emulators for 68k Macs, **Mini vMac** and **Basilisk II**.

These two have some similarities and some differences.

### Mini vMac

* <https://www.gryphel.com/c/minivmac/index.html>

This only emulates older 68k Macs and is available by default in two "variations", one which runs a Mac Plus and one which runs a Mac II:

* <https://www.gryphel.com/c/minivmac/download.html>

(there's also Mac 128K but that's so limiting as to be useless to me so I don't consider it)

You'll also want to get the [Blank Disk Images](https://www.gryphel.com/c/minivmac/extras/blanks/index.html). On Linux you can just make a blank disk image with `dd if=/dev/zero of=MyDisk.img bs=1M count=80` and vary the `count` depending on the size of the image.

The old Mac HFS file system can only store a maximum of 65536 files per filesystem, so don't create yourself a 4 GiB image and install everything on it. You're probably best to make a small "OS" image of about 100M and then confine future tinkering to additional hard drive images which you connect to the emulator as needed.

Mini vMac has no commandline options or configuration file. You can change some settings at runtime by holding the **Ctrl** key. If you want options applied permanently, you need to recompile it:

* <https://www.gryphel.com/c/minivmac/options.html>

This is actually very easy if you have a C compiler already setup on Linux. My preferences are:

```
setup_t -t lx64 -m Plus -magnify 1 -speed a -bg 1 > setup-plus.sh
setup_t -t lx64 -m II -magnify 1 -speed a -bg 1 > setup-ii.sh
```

To emulate a Mac Plus you will need a [Mac Plus ROM](https://archive.org/download/mac_rom_archive_-_as_of_8-19-2011/mac_rom_archive_-_as_of_8-19-2011.zip/4D1F8172%20-%20MacPlus%20v3.ROM) called `vMac.ROM` (case sensitive) in the same directory as the Mini vMac binary.

To emulate a Mac II you will need a [Mac II ROM](https://archive.org/download/mac_rom_archive_-_as_of_8-19-2011/mac_rom_archive_-_as_of_8-19-2011.zip/9779D2C4%20-%20MacII%20%28800k%20v2%29.ROM) called `MacII.ROM` (case sensitive) in the same directory as the Mini vMac binary.

To start Mini vMac, launch the binary and the screen will open showing the "Sad Mac" icon, this means the Mac cannot find a disk to boot from. Drag a floppy disk image or hard disk image onto the emulator window. The emulator does some live ROM patching magic to make the disk appear as plugged into the system, and the ROM will boot from the first disk you install.

The OS installation process is to boot from the `Install 1.img` file, then once the installer is complaining it can't find a valid hard disk, drag your hard disk image onto the emulation window and the installer will find it.

Once you have an OS installed on a disk, you can call that file `disk1.dsk` and Mini vMac will try to boot from it first any time you start it.

On the [Mini vMac Extra Software](https://www.gryphel.com/c/minivmac/extras/index.html) page you'll find these essentials:

* **ImportFl** which is used to get files into the emulated system from the host. As far as I can tell, this hooks the disk mount routine and instead saves the "new imported disk" to a file on the emulated OS.
* **ExportFl** which is used to get files out of the emulated system to the host. On Linux this makes a directory `out` wherever the emulator binary is.
* **binUnpk** which is used to unpack software in `.bin` files, and you'll be thankful any time you find these

Mini vMac is best if you can get disk images, unfortunately those are rare. We'll come back to getting more applications after looking at the next emulator.

### Basilisk II

* <https://basilisk.cebix.net/>

Basilisk definitely seems to emulate a Mac IIci and a Quadra 900 (which can run OS 8.x).

It seems you can select between running "pre-32-bit" Macs with the **Mac IIci** option, then selecting the appropriate CPU, RAM size, and ROM file, so you could probably emulate a Plus or SE or something else this way.

There's also a lot of confusing advice online about what ROM image works best, including vague statements like "the Performa ROM" (there are [78 models of Performa](https://en.wikipedia.org/wiki/Macintosh_Performa)).

In any case, you can try the advertised [Mac IIci ROM](https://archive.org/download/mac_rom_archive_-_as_of_8-19-2011/mac_rom_archive_-_as_of_8-19-2011.zip/368CADFE%20-%20Mac%20IIci.ROM) and [Quadra 900 ROM](https://archive.org/download/mac_rom_archive_-_as_of_8-19-2011/mac_rom_archive_-_as_of_8-19-2011.zip/420DBFF3%20-%20Quadra%20700%26900%20%26%20PB140%26170.ROM).

On Linux, you can get Basilisk II either as a [Flatpak on Flathub](https://flathub.org/apps/net.cebix.basilisk), or as an AppImage as listed at:

* <https://www.emaculation.com/forum/viewtopic.php?t=6580>
* <https://github.com/Korkman/macemu-appimage-builder/releases>

If you are using the AppImage and the theming goes all wonky so you can't read button labels due to a clash of light/dark themes, launch the AppImage like:

```
APP_GTK_THEME=no ./BasiliskII-x86_64.AppImage
```

I found Basilisk to be less reliable than Mini vMac, it hangs a lot (Use **Ctrl+Esc** to quit) or just crashes.

There are many hard-to-follow tutorials about using Basilisk:

* <https://www.emaculation.com/doku.php/sheepshaver_basiliskii_linux>
* <https://scruss.com/enterprise.net/basilisk_OS753.html>

Create your hard disk image in the Basilisk II interface.

Installing an OS is slightly different from Mini vMac. You need to boot from the `Disk Tools.img` floppy disk (included in 7.0 and 7.1 downloads) to format your hard drive image before the `Install 1.img` installer will recognise the disk.

Basilisk doesn't have a way to mount floppy disk images at runtime (at least on Linux it doesn't, apparently you can on Windows) which is mildly annoying, however it does have a **Unix Root** feature which creates a fake hard disk inside the emulator, the contents of which are a directory on the host filesystem.

This is both very convenient and very inconvenient. It's a great way to get files **into** the emulated OS because you can just drag and drop them, but it's not a very good way to get files **out** of the OS. Which brings us to...

## File Formats

Most Mac software you'll find is in one (or more) of these file formats:

* `bin` - MacBinary
* `hqx` - BinHex
* `sea` - Self Expanding Archive
* `smi` - Self-Mounting Image
* `sit` - StuffIt Expander compressed file (the Mac version of `zip` files)

On DOS and other OSes we're used to associating a file with an application by its extension, like a `.txt` is a text file to open with the text editor, a `.doc` is a document to open with a word processor, a `.png` is an image to open with a graphics program, etc. Mac OS doesn't work that way.

Mac OS has a hidden set of "metadata" about a file, such as its type and what application it should be opened with (it also stores other stuff like icons, graphics, dialog windows, etc). This is called the file's "[Resource Fork](https://en.wikipedia.org/wiki/Resource_fork)".

Unfortunately, only Mac's HFS and HFS+ filesystems have support for this metadata. There is no standard way to represent a Resource Fork to non-Mac systems with non-HFS filesystems, such as every other computer in existence.

So if you copy files out of the emulator using Mini vMac's **ExportFl** or Basilisk's Unix drive, you risk losing that metadata.

The solution is to put a file in one of the above container formats (`bin`/`hqx`) and name that container with the appropriate extension. So if you compress a Mac program into a BinHex file, then call the resulting file `MyProgram.hqx`. The vast majority of Mac software you download from the internet will be in one (or two, or more) of these formats. It's not incommon to download something like `program.img.bin.sit` which is a disk image, in a MacBinary file, compressed with StuffIt.

### StuffIt Expander

This is the standard compression and decompression utility on the Mac, much like DOS and Windows have WinZip, WinRar, 7-Zip, etc.

* <https://www.gryphel.com/c/sw/archive/stuffexp/index.html>
* <https://macintoshgarden.org/apps/stuffit-expander-55>
* <https://macintoshgarden.org/apps/stuffit-dropstuff-ee-45>
* <https://macintoshgarden.org/apps/stuffit-expander-402>

Version compatiblity is as follows:

* StuffIt 4.0 works on System 7.0
* StuffIt 4.5 works on System 7.0 but requires a 640x480 screen, so black-and-white Macs are out (unless you fake the emulator resolution to 640x480)
* StuffIt 5.5 requires System 7.1.1 or later, 68020 CPU, 8M RAM, and 640x480 screen, so you need a Mac II for this

There is also a common extension **DropStuff with Expander Enhancer** which helps if you want to make compressed files.

However, there is a problem.

An awful lot of Mac software you download from the internet was made with **newer versions** of StuffIt (presumably by people on OS8/OS9/OSX) which these older StuffIt Expander versions cannot read. You'll tell StuffIt 5.5 to uncompress something and you'll get either one lone file with no Resource Fork, or you'll get nothing.

As far as I can tell, the only way around this is... to emulate a newer Mac!

The [SheepShaver](https://sheepshaver.cebix.net/) emulator can emulate the PowerPC Macs require for such a thing, but I haven't gone that far down the rabbit hole yet.

## Software

For software you can find which usually works, look around these sites:

* [Macintosh Garden](https://macintoshgarden.org/) - less stuff but usually a bit curated and explained
* <https://www.gryphel.com/c/sw/> - the Mini vMac guy's page
* [Macintosh Repository](https://www.macintoshrepository.org/) - more stuff but less explained, has download limits
* [Mac GUI](https://www.macgui.com/downloads/)
* [Macintosh Library: The 4am and san inc Collection](https://archive.org/details/mac_library_4am?sort=-downloads) - cracked games
* <https://archive.org/download/ClassicMacImages> - a large random dump

### Essentials

You'll definitely want these:

* On Mini vMac: [ImportFl](https://www.gryphel.com/c/minivmac/extras/importfl/index.html), [ExportFl](https://www.gryphel.com/c/minivmac/extras/exportfl/index.html)
* [StuffIt Expander](https://www.gryphel.com/c/sw/archive/stuffexp/index.html) - for opening all sorts of compressed and image files
* [binUnpk](https://www.gryphel.com/c/minivmac/extras/binunpk/index.html) - for opening bin files (if StuffIt can't do it)
* [BinHex](https://www.gryphel.com/c/sw/archive/binhex/index.html) - for opening hqx files (if StuffIt can't do it)
* [Disk Copy](https://www.gryphel.com/c/sw/sysutils/diskcopy/index.html) - for mounting floppy disk images
* [Virtual CD-ROM Utility](https://macintoshgarden.org/apps/virtual-dvd-romcd-utility) - for mounting CD images like `ISO` or `toast`, needs big hard drive lots of RAM!

I also see these listed as essentials but I haven't had the need for them yet:

* [ResEdit](https://macintoshgarden.org/apps/resedit)
* [DropStuff](https://www.gryphel.com/c/sw/archive/dropstuf/index.html) - for creating compressed files

Once those are setup, can finally get into using the emulated computer and OS to do cool things.

### Applications

* [MacWrite](https://macintoshgarden.org/apps/macwrite) - was included by default with the first Mac 128K and was often the first program any Mac user ever tried
* [MacPaint](https://macintoshgarden.org/apps/macpaint) - was also included with the first Mac 128K and if the owner didn't start with MacWrite they started with this instead
* [BBEdit](https://macintoshgarden.org/search/node/bbedit) - a very popular text editor, it seems version 4 or 5 are the most popular

### Mac-only Games

There was a running joke in the 90s that Mac had no games, and it certainly had less than DOS/Windows (even C64/Amiga/Atari) and not very many good ones, but there were a few: 

* [Glider](https://macintoshgarden.org/games/glider-40) - paper plane action puzzle game, initially a free hobby, grew into a commercial game
* [Dark Castle](https://macintoshgarden.org/games/dark-castle) - platformer, uses WASD and mouse controls in 1986!
* [Systems Twilight](https://www.eblong.com/zarf/twilight/index.html) - puzzle game by Andrew Plotkin

### Mac-superior Games

There are even some games which were released on other platforms but are arguably better on the Mac:

* ICOM MacVentures - all released on the Mac first
    * [Deja Vu](https://macintoshgarden.org/games/deja-vu)
    * [Uninvited](https://macintoshgarden.org/games/uninvited)
    * [Shadowgate](https://macintoshgarden.org/games/shadowgate)
* [The Fool's Errand](https://macintoshgarden.org/games/the-fools-errand) - puzzle game inspired by real-life treasure hunts like [Masquerade](https://en.wikipedia.org/wiki/Masquerade_(book)), also made on the Mac first, then ported to DOS/Amiga which traded high resolution for more colours
* [The Manhole](https://macintoshgarden.org/games/the-manhole) - famous puzzle game made with HyperCard, by the Millers who would go on to write Myst

#### Mac-first Games

Some games were later ported elsewhere, but released first on the Mac:

* [Myst](https://macintoshgarden.org/games/myst) - the famous flick-screen puzzle adventure started on the Mac, as a HyperCard stack
* [SimCity](https://macintoshgarden.org/games/simcity) - I never expected it to look this great in black-and-white
* [Balance of Power](https://macintoshgarden.org/games/balance-of-power) and [1990 Edition](https://macintoshgarden.org/games/balance-of-power-the-1990-edition) - cold war geopolitical simulator by Chris Crawford
* [Exile: Escape from the Pit](https://macintoshgarden.org/games/exile-escape-from-the-pit) - fantastic RPG which I later played on Windows, remade (twice) as the modern [Avernum](https://store.steampowered.com/app/208400/Avernum_Escape_From_the_Pit/) series
* [Hidden Agenda](https://macintoshgarden.org/games/hidden-agenda) - another political strategy, even ported to DOS in black-and-white

#### Mac-interesting Games

There are games we're probably more used to playing elsewhere which saw release on the Mac:

* Space Quest [1](https://macintoshgarden.org/games/space-quest-1-original), [2](https://macintoshgarden.org/games/space-quest-2), [3](https://macintoshgarden.org/games/space-quest-3) - I'm so used to these on DOS EGA, it's a real trip to see them in black-and-white
* [Loom](https://macintoshgarden.org/games/loom) - I always associated this game with being coloruful, again strange to see in black-and-white
* [Starflight](https://macintoshgarden.org/games/starflight) - this great open-world sci-fi RPG was everywhere wasn't it?
* [Where in Europe is Carmen Sandiego?](https://macintoshgarden.org/games/where-in-europe-carmen-sandiego) - I played a lot of this on DOS in CGA, higher res B&W is arguably better

#### More Research Required

These caught my eye as possibly interesting:

* [Beached](https://macintoshgarden.org/games/beached) and [Beached II](https://macintoshgarden.org/games/beached-ii) - isometric strategy/survival game
* [TaskMaker](https://macintoshgarden.org/games/taskmaker) - Ultima-like tile-based RPG
* [Full Metal Planete](https://macintoshgarden.org/games/full-metal-planet) - awesome looking sci-fi hex strategy game, so popular it was made into a board game
* [The Dungeon of Doom](https://macintoshgarden.org/games/the-dungeon-of-doom) and [The Dungeon Revealed](https://macintoshgarden.org/games/the-dungeon-revealed) - tile-based roguelikes
* [Voyager](https://macintoshgarden.org/apps/voyager-the-interactive-desktop-planetarium) and [Voyager II](https://macintoshgarden.org/apps/voyager-ii) - interactive planetariums
* Jaunt Trooper [Mission Thunderbolt](https://macintoshgarden.org/games/mission-thunderbolt) and [Mission Firestorm](https://macintoshgarden.org/games/jaunttrooper-mission-firestorm) - a remake of a mainframe roguelike called Doomsday 2000
* [Beyond Cyberpunk: A Do-It-Yourself Guide to the Future](https://macintoshgarden.org/apps/beyond-cyberpunk-a-do-it-yourself-guide-the-future) - a cyberpunk manifesto in HyperCard on five floppies?

## OS Tinkering

Mac OS is very customisable. If one has the programming skill it seems possible to change almost any aspect.

The components to do this were called "INITs" up to System 6, and "System Extensions" on System 7+.

There are also Control Panel Devices (aka "CDEVs") which add things into the system Control Panel.

You can get lots of ideas of what these are capable of from pre-installed OS images like these:

* [Mac OS Enhanced](https://macintoshgarden.org/apps/maciienhanced608) - system 6 and 7 from the person who invented the [MOOF disk image format](https://applesaucefdc.com/moof-reference/)
* [Macintosh Downloads](https://www.savagetaylor.com/downloads/downloads-macintosh/) - floppy and hard drive images for old and new real hardware and emulators

There were also silly "joke" system extensions, such as [Enchanted Menus 88](https://macintoshgarden.org/apps/enchanted-menus-88) which just opens the top-bar menus at a random location on the screen.

This and more are detailed in the books:

* [Stupid Mac Tricks (1990)](https://macintoshgarden.org/apps/stupid-mac-tricks)
* [Son of Stupid Mac Tricks (1991)](https://macintoshgarden.org/apps/son-of-stupid-mac-tricks)
* [This Mac is MINE (1992)](https://macintoshgarden.org/apps/mac-mine)

## Developing on/for the Mac

### Inside Macintosh

Apple published the Inside Macintosh series of books describing the OS API in detail:

* <https://en.wikipedia.org/wiki/Inside_Macintosh>
* <https://archive.org/download/inside-macintosh-1992-1994>

Of particular interest is the [Human Interface Guidelines](https://archive.org/download/inside-macintosh-1992-1994/1992-human_interface_guidelines.pdf) book.  Steve Jobs had a vision for how people should interact with computers. To help other developers get into the same mindset and steer all Mac applications to a common set of GUI idioms, this book explains how to lay out an application with fantastic diagrams, and even goes into detail on how to design for different languages, disabilities, to test software, and work with people evaluating your program. It's a fascinating book to flip through.

### Macintosh Programmer's Workshop (MPW)

Apple wrote the OS and their programs in 68k assembly and Pascal at first, but later moved to C with the change to 32-bit and the PowerPC platform.

MPW seems to be what Apple used? It seems to have grown over time with their needs and was eventually replaced by CodeWarrior:

* <https://en.wikipedia.org/wiki/Macintosh_Programmer%27s_Workshop>

### HyperCard

Many amateurs at home got a start by tinkering with HyperCard, which is an interesting combination of slideshow, database, hypertext, and scripting language. You'll find many adventure games written in HyperCard. As mentioned above, The Manhole was written in HyperCard which later resulted in Myst!

* <https://en.wikipedia.org/wiki/HyperCard>
* <https://macintoshgarden.org/apps/hypercard>
* <https://macintoshgarden.org/apps/hypercard-player>

### BASIC

BASIC was also popular around this time. Some of the original Macintosh team members developed MacBASIC, which not only implemented the programming language but allowed a BASIC API to control native system UI like windows and buttons:

* <https://en.wikipedia.org/wiki/MacBASIC>
* <https://macintoshgarden.org/apps/macbasic-10>
* <https://macintoshgarden.org/apps/vintage-macbasic-books>

Microsoft Basic for Mac was originally criticized for lacking support for the Macintosh Toolbox native UI, but this was resolved by MS Basic 3. That was combined with the compiler into Microsoft QuickBASIC for Mac:

* <https://winworldpc.com/product/quickbasic/10x-for-mac>

### C

Lightspeed C, which became THINK C then Symantec C, seems to have been the most popular at the time. It's definitely not like a traditional UNIX environment with Makefiles, but if you follow the manual you can compile a program linked with the OS libraries easily enough.

* <https://en.wikipedia.org/wiki/THINK_C>
* <https://winworldpc.com/product/think-c>
* <https://macintoshgarden.org/search/node/Think%20C>

C support was later added to MPW (above), and another successful C environment was CodeWarrior:

* <https://en.wikipedia.org/wiki/CodeWarrior>

If you want to write in C for the Mac today, the nicest tools seem to be the Retro68 GCC cross-compiler:

* <https://github.com/autc04/Retro68>
* <https://www.toughdev.com/content/2017/03/exploring-retro68-gcc-based-sdk-for-68k-macintoshes/>
* <https://henlin.net/2021/12/03/a-simplified-guide-to-development-using-retro68-and-pce-macplus/>

### Pascal

I don't know much about Pascal so I'm just going to drop some links:

* <https://winworldpc.com/product/think-pascal>
* <http://www.think-pascal.org/>
* <https://wiki.lazarus.freepascal.org/Category:Mac_OS_Classic>
* <https://archive.org/details/THINKPascalUserManual1991>

## Go Forth and Mac!

Hopefully that's enough to get you started on emulating Classic Macs and exploring the unique software ecosystem.

Some YouTube channels with good videos about Macs are:

* [Macintosh Librarian](https://www.youtube.com/@MacintoshLibrarian)
* [This Does Not Compute](https://www.youtube.com/@ThisDoesNotCompute)
* [Adrian's Digital Basement](https://www.youtube.com/@adriansdigitalbasement)
* [Action Retro](https://www.youtube.com/@ActionRetro)
* [Classic Mac Gaming](https://www.youtube.com/@insanelygruz)
