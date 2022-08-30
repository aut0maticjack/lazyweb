This grew into PPAs, repos, and packages, but whatever.

Current to version: **Ubuntu 22.04 (jammy)**

# PPAs

### Firefox - web browser

Because the snap takes like 15 seconds to launch smh

https://balintreczey.hu/blog/firefox-on-ubuntu-22-04-from-deb-not-from-snap/

https://launchpad.net/%7Emozillateam/+archive/ubuntu/ppa?field.series_filter=jammy

    /etc/apt/preferences.d/firefox-no-snap 
    Package: firefox*
    Pin: release o=Ubuntu*
    Pin-Priority: -1

Then

    sudo apt purge firefox
    sudo snap remove firefox
    sudo add-apt-repository ppa:mozillateam/ppa
    sudo apt update
    sudo apt install firefox

### git - Distributed Version Control System

https://launchpad.net/~git-core/+archive/ubuntu/ppa?field.series_filter=jammy

    sudo add-apt-repository ppa:git-core/ppa
    sudo apt install git git-email

### Inkscape - vector graphics editor

https://launchpad.net/~inkscape.dev/+archive/ubuntu/stable?field.series_filter=jammy

    sudo add-apt-repository ppa:inkscape.dev/stable
    sudo apt install inkscape

### KeePassXC - password manager

https://launchpad.net/~phoerious/+archive/ubuntu/keepassxc?field.series_filter=jammy

    sudo add-apt-repository ppa:phoerious/keepassxc
    sudo apt install keepassxc

### Mesa - 3D stuff

https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa?field.series_filter=jammy

    sudo add-apt-repository ppa:kisak/kisak-mesa
    sudo apt update

To remove:

    sudo apt install ppa-purge
    sudo ppa-purge ppa:kisak/kisak-mesa

If this breaks, alternative "stable" repo at:

 https://launchpad.net/~kisak/+archive/ubuntu/turtle/?field.series_filter=jammy

### RetroArch - multi-platform emulator frontend and framework

https://launchpad.net/~libretro/+archive/ubuntu/stable?field.series_filter=jammy

    sudo apt-add-repository ppa:libretro/stable
    sudo apt install retroarch retroarch-assets

There's also a testing/nightly repo if you feel like updating hundreds of MiB of cores every day:

https://launchpad.net/~libretro/+archive/ubuntu/testing?field.series_filter=jammy

    sudo add-apt-repository ppa:libretro/testing

Probably better to install cores thru the web downloader.

### PCSX2 - PlayStation 2 emulator

https://launchpad.net/~pcsx2-team/+archive/ubuntu/pcsx2-daily?field.series_filter=jammy

    sudo dpkg --add-architecture i386
    sudo add-apt-repository ppa:pcsx2-team/pcsx2-daily
    sudo apt install pcsx2

### PPSSPP - PlayStation Portable emulator

https://launchpad.net/~xuzhen666/+archive/ubuntu/ppsspp?field.series_filter=jammy

    sudo add-apt-repository ppa:xuzhen666/ppsspp
    sudo apt install ppsspp

Get the fonts from [Sony's 6.61 firmware](http://de01.psp.update.playstation.org/update/psp/image/eu/2014_1212_6be8878f475ac5b1a499b95ab2f7d301/EBOOT.PBP) and put in the `flash0/font` directory.

### Transmission - Torrent Client

https://launchpad.net/~transmissionbt/+archive/ubuntu/ppa?field.series_filter=focal

    sudo add-apt-repository ppa:transmissionbt/ppa
    sudo apt install transmission

### UNetBootin - LiveUSB creator

https://launchpad.net/~gezakovacs/+archive/ubuntu/ppa?field.series_filter=focal

    sudo apt-add-repository ppa:gezakovacs/ppa
    sudo apt install unetbootin

### Wireshark - packet capture analysis tool

https://launchpad.net/~wireshark-dev/+archive/ubuntu/stable?field.series_filter=jammy

    sudo apt-add-repository ppa:wireshark-dev/stable
    sudo apt install wireshark

### Zim - desktop wiki

https://launchpad.net/~jaap.karssenberg/+archive/ubuntu/zim?field.series_filter=jammy

    sudo add-apt-repository ppa:jaap.karssenberg/zim
    sudo apt install zim

----

# Repositories

### Mopidy - MPD-compatible music daemon

https://docs.mopidy.com/en/latest/installation/debian/

    wget -q -O - https://apt.mopidy.com/mopidy.gpg | sudo apt-key add -
    sudo wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/buster.list
    sudo apt update
    sudo apt install mopidy mopidy-mpd

### Spotify

    curl -sS https://download.spotify.com/debian/pubkey_5E3C45D7B312C643.gpg | sudo apt-key add - 
    echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list

https://www.spotify.com/au/download/linux/

### WINE - Windows API compatibility layer

https://wiki.winehq.org/Ubuntu

    sudo dpkg --add-architecture i386
    wget -nc https://dl.winehq.org/wine-builds/winehq.key
    sudo mv winehq.key /usr/share/keyrings/winehq-archive.key    
    wget -nc https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
    sudo mv winehq-jammy.sources /etc/apt/sources.list.d/
    sudo apt update
    sudo apt install --install-recommends winehq-devel

----

# Packages

### HakuNeko S - manga downloader

https://sourceforge.net/projects/hakuneko/

### OpenXcom - turn-based strategy game

AppImages of nightlies on the website:

https://openxcom.org/git-builds/

### Krita - photo editor

AppImages:

https://krita.org/en/download/krita-desktop/

### RetroArch - emulators

https://buildbot.libretro.com/stable/

### Steam - games

https://store.steampowered.com/about/

Also, [Proton Requirements](https://github.com/ValveSoftware/Proton/wiki/Requirements) suggests to install:

https://launchpad.net/~kisak/+archive/ubuntu/kisak-mesa

    sudo add-apt-repository ppa:kisak/kisak-mesa

### Ubuntu Kernel

https://kernel.ubuntu.com/~kernel-ppa/mainline/
