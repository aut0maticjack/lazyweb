This grew into PPAs, repos, packages, and now Flatpaks, but whatever.

Current to version: **Ubuntu 22.04 (jammy)**

## PPAs

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

### Flatpak - Application packaging (not a sandbox)

https://launchpad.net/~flatpak/+archive/ubuntu/stable?field.series_filter=jammy

    sudo add-apt-repository ppa:flatpak/stable
    sudo apt install flatpak

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

### Linux Mint xapps

Great tidy non-desktop-specific tools made by Linux Mint devs

https://launchpad.net/~kelebek333/+archive/ubuntu/mint-tools?field.series_filter=jammy

    sudo add-apt-repository ppa:kelebek333/mint-tools
    sudo apt install bulky  # bulk renamer
    sudo apt install xed    # text editor

### Lutris - game launcher

https://launchpad.net/~lutris-team/+archive/ubuntu/lutris?field.series_filter=jammy

    sudo add-apt-repository ppa:lutris-team/lutris
    sudo apt install lutris

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

## Repositories

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

### Visual Studio Code - Fancy text editor

https://code.visualstudio.com/docs/setup/linux

    sudo apt-get install wget gpg
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
    sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
    rm -f packages.microsoft.gpg
    sudo apt install apt-transport-https
    sudo apt update
    sudo apt install code
    mkdir -p ~/.Code/User/
    cat <<EOT >> ~/.config/Code/User/settings.json
    {
        "telemetry.telemetryLevel": "off",
        "workbench.editor.enablePreview": false,
    }
    EOT


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

## Packages

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

----

## Flatpak

### Flatseal - permissions manager

https://flathub.org/apps/details/com.github.tchx84.Flatseal

    flatpak install flathub com.github.tchx84.Flatseal

### Spotify - music

https://flathub.org/apps/details/com.spotify.Client

    flatpak install flathub com.spotify.Client

----

## Flatpak Games

### dosbox-staging - MS-DOS emulator

https://flathub.org/apps/details/io.github.dosbox-staging

    flatpak install flathub io.github.dosbox-staging

### DOSBox-X - MS-DOS emulator

https://flathub.org/apps/details/com.dosbox_x.DOSBox-X

    flatpak install flathub com.dosbox_x.DOSBox-X

### DuckStation - the best PSX emulator

https://flathub.org/apps/details/org.duckstation.DuckStation

    flatpak install flathub org.duckstation.DuckStation

### Gargoyle - interactive fiction player

https://flathub.org/apps/details/io.github.garglk.Gargoyle

    flatpak install flathub io.github.garglk.Gargoyle

### Lutris - game runner

https://flathub.org/apps/details/net.lutris.Lutris

    flatpak install flathub net.lutris.Lutris

### mGBA - GBA emulator

https://flathub.org/apps/details/io.mgba.mGBA

    flatpak install flathub io.mgba.mGBA

### OpenRA - real time strategy

https://flathub.org/apps/details/net.openra.OpenRA

    flatpak install flathub net.openra.OpenRA

### OpenTTD - train anoraks

https://flathub.org/apps/details/org.openttd.OpenTTD

    flatpak install flathub org.openttd.OpenTTD

### OpenTyrian - shooter

https://flathub.org/apps/details/com.github.opentyrian.OpenTyrian

    flatpak install flathub com.github.opentyrian.OpenTyrian

### PCSX2 - PlayStation 2 emulator

https://flathub.org/apps/details/net.pcsx2.PCSX2

    flatpak install flathub net.pcsx2.PCSX2

### PPSSPP - PlayStation Portable emulator

https://flathub.org/apps/details/org.ppsspp.PPSSPP

    flatpak install flathub org.ppsspp.PPSSPP

### RetroArch - multi emulator

https://flathub.org/apps/details/org.libretro.RetroArch

    flatpak install flathub org.libretro.RetroArch

### ScummVM - adventure games

https://flathub.org/apps/details/org.scummvm.ScummVM

    flatpak install flathub org.scummvm.ScummVM
