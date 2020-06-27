This grew into PPAs, repos, and packages, but whatever.

Current to version: **Ubuntu 20.04 (focal)**

## PPAs

### GIMP - GNU Image Manipulation Program

https://launchpad.net/~otto-kesselgulasch/+archive/ubuntu/gimp?field.series_filter=focal

    sudo add-apt-repository ppa:otto-kesselgulasch/gimp
    sudo apt install gimp

### Mesa - 3D stuff

https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa?field.series_filter=focal

    sudo add-apt-repository ppa:kisak/kisak-mesa
    sudo apt update

To remove:

    sudo apt install ppa-purge
    sudo ppa-purge ppa:kisak/kisak-mesa

If this breaks, alternative "stable" repo at:

 https://launchpad.net/~kisak/+archive/ubuntu/turtle/?field.series_filter=focal

### RetroArch - multi-platform emulator frontend and framework

https://launchpad.net/~libretro/+archive/ubuntu/stable?field.series_filter=focal

    sudo apt-add-repository ppa:libretro/stable
    sudo apt install retroarch retroarch-assets

There's also a testing/nightly repo if you feel like updating hundreds of MiB of cores every day:

https://launchpad.net/~libretro/+archive/ubuntu/testing?field.series_filter=focal

    sudo add-apt-repository ppa:libretro/testing

Probably better to install cores thru the web downloader.

### Transmission - Torrent Client

https://launchpad.net/~transmissionbt/+archive/ubuntu/ppa?field.series_filter=focal

    sudo add-apt-repository ppa:transmissionbt/ppa
    sudo apt install transmission

### UNetBootin - LiveUSB creator

https://launchpad.net/~gezakovacs/+archive/ubuntu/ppa?field.series_filter=focal

    sudo apt-add-repository ppa:gezakovacs/ppa
    sudo apt install unetbootin

### Wireshark - packet capture analysis tool

https://launchpad.net/~wireshark-dev/+archive/ubuntu/stable?field.series_filter=focal

    sudo apt-add-repository ppa:wireshark-dev/stable
    sudo apt install wireshark

## Repositories

### Mopidy - MPD-compatible music daemon

https://docs.mopidy.com/en/latest/installation/debian/

    wget -q -O - https://apt.mopidy.com/mopidy.gpg | sudo apt-key add -
    sudo wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/buster.list
    sudo apt update
    sudo apt install mopidy mopidy-mpd

### WINE - Windows API compatibility layer

https://wiki.winehq.org/Ubuntu

    sudo dpkg --add-architecture i386
    wget -O - https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -
    sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main' 
    sudo apt update
    sudo apt install --install-recommends winehq-stable

## Packages

### HakuNeko S - manga downloader

https://sourceforge.net/projects/hakuneko/

### OpenXcom - turn-based strategy game

AppImages of nightlies on the website:

https://openxcom.org/git-builds/

### Steam - games

https://store.steampowered.com/about/

Also, [Proton Requirements](https://github.com/ValveSoftware/Proton/wiki/Requirements) suggests to install:

https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa

    sudo add-apt-repository ppa:kisak/kisak-mesa

### Ubuntu Kernel

https://kernel.ubuntu.com/~kernel-ppa/mainline/
