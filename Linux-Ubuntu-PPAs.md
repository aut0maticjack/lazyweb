This grew into PPAs, repos, and packages, but whatever.

Current to version: **Ubuntu 18.04 (bionic)**

## PPAs

### Atom - text editor

https://launchpad.net/~webupd8team/+archive/ubuntu/atom?field.series_filter=bionic

    sudo apt-add-repository ppa:webupd8team/atom
    sudo apt install atom

### FreeCAD - parametric 3D modeler

https://launchpad.net/~freecad-maintainers/+archive/ubuntu/freecad-stable?field.series_filter=bionic

    sudo apt-add-repository ppa:freecad-maintainers/freecad-stable
    sudo apt install freecad

### FS-UAE - Amiga Emulator

(same version available in repo as of Feb 2019)

https://launchpad.net/~fengestad/+archive/ubuntu/stable?field.series_filter=bionic

    sudo apt-add-repository ppa:fengestad/stable
    sudo apt install fs-uae fs-uae-arcade fs-uae-launcher

### GIMP - GNU Image Manipulation Program

https://launchpad.net/~otto-kesselgulasch/+archive/ubuntu/gimp?field.series_filter=bionic

    sudo add-apt-repository ppa:otto-kesselgulasch/gimp
    sudo apt install gimp

### Inkscape - vector drawing tool

(same major version available in repo as of Feb 2019)

https://launchpad.net/~inkscape.dev/+archive/ubuntu/stable?field.series_filter=bionic

    sudo add-apt-repository ppa:inkscape.dev/stable
    sudo apt install inkscape

### Krita - paint program

https://launchpad.net/~kritalime/+archive/ubuntu/ppa?field.series_filter=bionic

    sudo add-apt-repository ppa:kritalime/ppa
    sudo apt install krita

### OpenXcom - turn-based strategy game

This has a "stable" but the project doesn't have much stable/milestone activity:

https://launchpad.net/~knapsu/+archive/ubuntu/openxcom?field.series_filter=bionic

    sudo add-apt-repository ppa:knapsu/openxcom
    sudp apt install openxcom

There are AppImages of nightlies on the website:

https://openxcom.org/git-builds/

### RetroArch - multi-platform emulator frontend and framework

https://launchpad.net/~libretro/+archive/ubuntu/stable?field.series_filter=bionic

    sudo apt-add-repository ppa:libretro/stable
    sudo apt install retroarch libretro-<whatever>

There's also a testing/nightly repo if you feel like updating hundreds of MiB of cores every day:

https://launchpad.net/~libretro/+archive/ubuntu/testing?field.series_filter=bionic

    sudo add-apt-repository ppa:libretro/testing

### Transmission - Torrent Client

https://launchpad.net/~transmissionbt/+archive/ubuntu/ppa?field.series_filter=bionic

    sudo add-apt-repository ppa:transmissionbt/ppa
    sudo apt install transmission-cli transmission-common transmission-daemon

### UNetBootin - LiveUSB creator

https://launchpad.net/~gezakovacs/+archive/ubuntu/ppa?field.series_filter=bionic

    sudo apt-add-repository ppa:gezakovacs/ppa
    sudo apt install unetbootin

### webupd8 - Lots of different packages

Haven't looked at this for bionic yet

https://launchpad.net/~nilarimogard/+archive/ubuntu/webupd8?field.series_filter=xenial

    sudo apt-add-repository ppa:nilarimogard/webupd8
    sudo apt install ncmpcpp

### Wireshark - packet capture analysis tool

https://launchpad.net/~wireshark-dev/+archive/ubuntu/stable?field.series_filter=bionic

    sudo apt-add-repository ppa:wireshark-dev/stable
    sudo apt install wireshark tshark

## Repositories

### Mopidy - MPD-compatible music daemon

https://docs.mopidy.com/en/latest/installation/debian/

    wget -q -O - https://apt.mopidy.com/mopidy.gpg | sudo apt-key add -
    sudo wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/stretch.list
    sudo apt update
    sudo apt install mopidy

### OpenSCAD - constructive solid geometry 3D modeler

Official nightlies

    wget -qO - http://files.openscad.org/OBS-Repository-Key.pub | sudo apt-key add -
    echo 'deb http://download.opensuse.org/repositories/home:/t-paul/xUbuntu_18.04/ ./' | sudo tee -a /etc/apt/sources.list.d/openscad.list
    sudo apt update
    sudo apt install openscad-nightly

### QCMA - used to copy files to PS Vita

https://codestation.github.io/qcma/

    wget -q0 - https://download.opensuse.org/repositories/home:codestation/xUbuntu_18.04/Release.key | sudo apt-key add -
    echo 'deb http://download.opensuse.org/repositories/home:/codestation/xUbuntu_18.04/ /' | sudo tee -a /etc/apt/sources.list.d/qcma.list
    sudo apt update
    sudo apt install qcma

### WINE - Windows API compatibility layer

Haven't played with this in 18.04 but here's the old 16.04 instructions

https://www.winehq.org/pipermail/wine-devel/2017-March/117104.html

    wget https://dl.winehq.org/wine-builds/Release.key
    sudo apt-key add Release.key
    sudo apt-add-repository 'https://dl.winehq.org/wine-builds/ubuntu/'

No idea what to install.

## Packages

### Google Chrome - web browser

https://www.google.com/chrome

### HakuNeko S - manga downloader

https://sourceforge.net/projects/hakuneko/

### Midori - lightweight web browser

http://midori-browser.org/download/ubuntu/

Distributing as a snap now:

https://snapcraft.io/midori

### Steam - games

https://store.steampowered.com/about/

### Ubuntu Kernel

https://kernel.ubuntu.com/~kernel-ppa/mainline/
