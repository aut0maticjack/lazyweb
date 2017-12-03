This grew into PPAs, repos, and packages, but whatever

## PPAs

~~~sh
# Atom - text editor
# https://launchpad.net/~webupd8team/+archive/ubuntu/atom?field.series_filter=xenial
sudo apt-add-repository ppa:webupd8team/atom
# sudo apt install atom

# FreeCAD - parametric 3D modeler
# https://launchpad.net/~freecad-maintainers/+archive/ubuntu/freecad-stable?field.series_filter=xenial
sudo apt-add-repository ppa:freecad-maintainers/freecad-stable
# sudo apt install freecad

# FS-UAE - Amiga Emulator
# https://launchpad.net/~fengestad/+archive/ubuntu/stable?field.series_filter=xenial
sudo apt-add-repository ppa:fengestad/stable
# sudo apt install fs-uae fs-uae-arcade fs-uae-launcher

# GIMP - GNU Image Manipulation Program
# https://launchpad.net/~otto-kesselgulasch/+archive/ubuntu/gimp?field.series_filter=xenial
sudo add-apt-repository ppa:otto-kesselgulasch/gimp
# sudo apt install gimp
# 
# also a nightly/edge repo available:
# https://launchpad.net/~otto-kesselgulasch/+archive/ubuntu/gimp-edge?field.series_filter=xenial
# sudo add-apt-repository ppa:otto-kesselgulasch/gimp-edge
# Google - Chrome and other even internet overlordship
# https://www.google.com/linuxrepositories/
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
# sudo apt install google-chrome-stable

# Inkscape - vector drawing tool
# https://launchpad.net/~inkscape.dev/+archive/ubuntu/stable?field.series_filter=xenial
sudo add-apt-repository ppa:inkscape.dev/stable
# sudo apt install inkscape

# Mopidy - MPD-compatible music daemon
# https://docs.mopidy.com/en/latest/installation/debian/
wget -q -O - https://apt.mopidy.com/mopidy.gpg | sudo apt-key add -
sudo wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/jessie.list
# sudo apt install mopidy mopidy-youtube

# OpenSCAD - constructive solid geometry 3D modeler
# https://launchpad.net/~openscad/+archive/ubuntu/releases?field.series_filter=xenial
sudo apt-add-repository ppa:openscad/releases
# sudo apt install openscad

# OpenXcom - turn-based strategy game
# https://launchpad.net/~winterheart/+archive/ubuntu/openxcom?field.series_filter=xenial
sudo apt-add-repository ppa:winterheart/openxcom
# sudo apt install openxcom
# 
# there's also these "official" repos by the developer, but they are not frequently updated:
# https://launchpad.net/~knapsu/+archive/ubuntu/openxcom?field.series_filter=xenial
# https://launchpad.net/~knapsu/+archive/ubuntu/openxcom-beta?field.series_filter=xenial

# Qt 5.6 - needed for Simplify3D 4.0 to work on Xenial
# https://launchpad.net/~beineri/+archive/ubuntu/opt-qt562-xenial?field.series_filter=xenial
sudo apt-add-repository ppa:beineri/opt-qt562-xenial
# sudo apt install qt56-meta-full

# RetroArch - multi-platform emulator frontend and framework
# https://launchpad.net/~libretro/+archive/ubuntu/stable?field.series_filter=xenial
sudo apt-add-repository ppa:libretro/stable
# sudo apt install retroarch libretro-<whatever>
# 
# there's also a testing/nightly repo if you feel like updating hundreds of mib of cores every day:
# https://launchpad.net/~libretro/+archive/ubuntu/testing?field.series_filter=xenial

# UNetBootin - LiveUSB creator
# https://launchpad.net/~gezakovacs/+archive/ubuntu/ppa?field.series_filter=xenial
sudo apt-add-repository ppa:gezakovacs/ppa
# sudo apt install unetbootin

# webupd8 - Lots of different packages
# https://launchpad.net/~nilarimogard/+archive/ubuntu/webupd8?field.series_filter=xenial
sudo apt-add-repository ppa:nilarimogard/webupd8
# sudo apt install ncmpcpp

# Wireshark - packet capture analysis tool
# https://launchpad.net/~wireshark-dev/+archive/ubuntu/stable?field.series_filter=xenial
sudo apt-add-repository ppa:wireshark-dev/stable
# sudo apt install wireshark
~~~

## Repositories

~~~sh
# OpenVPN - VPN client/server
# https://community.openvpn.net/openvpn/wiki/OpenvpnSoftwareRepos
sudo -s
wget -O - https://swupdate.openvpn.net/repos/repo-public.gpg|apt-key add -
echo "deb http://build.openvpn.net/debian/openvpn/stable xenial main" > /etc/apt/sources.list.d/openvpn-aptrepo.list
sudo apt install openvpn

# WINE - Windows API compatibility layer
# https://www.winehq.org/pipermail/wine-devel/2017-March/117104.html
wget https://dl.winehq.org/wine-builds/Release.key
sudo apt-key add Release.key
sudo apt-add-repository 'https://dl.winehq.org/wine-builds/ubuntu/'
# no idea what to install
~~~

## Packages

~~~sh
# mate-calc - the best calculator
# Not actually a PPA, just get mate-calc-common and mate-calc from the Linux Mint repos
# http://packages.linuxmint.com/
wget http://packages.linuxmint.com/pool/backport/m/mate-calc/mate-calc_1.18.1-1+sonya_amd64.deb
wget http://packages.linuxmint.com/pool/backport/m/mate-calc/mate-calc-common_1.18.1-1+sonya_all.deb
~~~