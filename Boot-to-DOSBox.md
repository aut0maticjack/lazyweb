## Overview

This is a set of instructions to create a minimal bootable LiveUSB which runs Linux but boots to DOSBox so you appear to have a DOS computer. This allows you to carry around DOS games and play them on most modern desktops and laptops.

* **Author:** Jamie Bainbridge - jamie.bainbridge@gmail.com
* **License:** [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/)

## Requirements

* Ubuntu Mini Remix - http://www.ubuntu-mini-remix.org/ - pick the 16.04 i386 image
* Unetbootin - http://unetbootin.github.io/
* A PC with internet access, at least to get DOSBox working and some games on there
* USB drive, 4 GiB or 8 GiB is fine (see [note](#note-about-usb-drive-size) below)
* Some basic knowledge of Linux text editing with `nano` or `vim` and `sudo`. If you don't know this then search Google for "linux nano tutorial" and "linux sudo tutorial".
* An understanding of DOSBox and [its configuration file](http://www.dosbox.com/wiki/dosbox.conf)

## Create a Bootable Drive with Persistent Storage

Format the USB drive as FAT32.

Ensure the first partition is bootable. In Linux use `fdisk` and toggle bootable flag with **a**. In Windows use `diskpart` and set **active**.

Use UNetbootin to put the Ubuntu Mini Remix image onto the USB drive. Give up to 4000 MiB persistent space.

See the [note](#note-about-usb-drive-size) below to understand why you can't add more space than that.

## Network

Plug Ethernet in before boot.

## WiFi (untested)

Find your wireless device name with `ip addr`. If you don't see a wireless device I'd assume your wireless card is not supported in Linux, or you need Ethernet to install more stuff to get the wireless to work, which is beyond the scope of this tutorial.

If you do have a wireless device, I'll assume it's `wlan0`, edit `/etc/network/interfaces` as below:

    auto lo 
    iface lo inet loopback

    iface eth0 inet dhcp

    allow-hotplug wlan0
    auto wlan0
    iface wlan0 inet dhcp
        wpa-ssid "SSID"
        wpa-psk  "Password"
        wireless-power off
    iface default inet dhcp

Reboot.

## Install DOSBox

The default login name is `ubuntu` with a blank password.

Make a directory to be the DOSBox C drive: `mkdir ~/DOS`

In `/etc/apt/sources.list` add `universe multiverse` to the end of each repo line.

Update repos: `sudo apt update`

Install stuff: `sudo apt install dosbox alsa-base pulseaudio vim`

Run just `dosbox` to make a base config file.

This will look like messy text so type `EXIT` and press **Enter**, then **Ctrl+l** (lowercase L) to clear the terminal.

Run `sudo dosbox` and it should run much better on the framebuffer. Type `EXIT` and press **Enter**.

Edit `~/.dosbox/dosbox-0.74.conf` as below:

    output=overlay
    usescancodes=false

    aspect=true
    scaler=normal2x
    # you can use the others like hq2x or advmame2x if you like them
    # you can use 3x if your screen is big enough

    cycles=25000
    # the ideal cycles number will depend on your computer and game
    cycleup=2500
    cycledown=2500

    [autoexec]
    @ECHO OFF
    MOUNT C ~/DOS
    C:

Run `sudo dosbox` again to test your settings. Repeat until you're happy with it.

## Auto Login

`sudo mkdir -p /etc/systemd/system/getty@tty1.service.d/`

Edit `/etc/systemd/system/getty@tty1.service.d/autologin.conf` as below:

    [Service]
    ExecStart=
    ExecStart=-/sbin/agetty --autologin ubuntu --noclear %I \$TERM

## Auto Start DOSBox

Edit `/etc/profile.d/10-runthing.sh` as below:

    if [ "$(tty)" = "/dev/tty1" ]; then
        sudo dosbox
    fi

## Copying Games via Network (Recommended Method)

Install SSH server: `sudo apt install openssh-server`

Start SSH server: `sudo systemctl start sshd`

Make SSH server start on boot: `sudo systemctl enable sshd`

Change user password: `sudo passwd ubuntu` and set the password to `password` or whatever you like.

Type `ip address` if you need to know the LiveUSB system's IP.

Use a graphical SFTP program like [Filezilla](https://filezilla-project.org/) (Lin/Win/Mac) or [WinSCP](https://winscp.net/) (Win) or [CyberDuck](https://cyberduck.io/) (Mac) to copy games to `/home/ubuntu/DOS/` on the LiveUSB system.

The username is `ubuntu` and the password is `password` or whatever you set above.

If you copy new games on while DOSBox is running, press **Ctrl+F4** within DOSBox to refresh the files from disk.

## To Turn Off

Always shut down properly, don't just turn the power off and yank the USB drive out. If you do that, you may lose any changes you've made (like saved games) or corrupt the persistent storage.

Exit DOSBox with `EXIT` or **Ctrl+F9**.

Turn the real computer's power off with: `sudo poweroff`

## Speed Control

Turn DOSBox cycles down with **Ctrl+F11**, the number of cycles corresponds to `cycledown` in the config file.

Turn DOSBox cycles up with **Ctrl+F12**, the number of cycles corresponds to `cycleup` in the config file.

You can also set a cycles value inside DOSBox with a command like: `CYCLES 10000`

## Volume Control

Run `MIXER` inside DOSBox.

You can also use `alsamixer` on the Linux commandline.

## Mouse Support

Dowload [CuteMouse](http://cutemouse.sourceforge.net/) and run it inside DOSBox with `CTMOUSE`

You could add that command to the `[autoexec]` section in `dosbox.conf` if you like.

You can adjust mouse sensitivity like `CTMOUSE /R5`, the R number can be 1 to 9 (0 is auto).

You can also adjust mouse sensitivity with `sensitivity` setting in `dosbox.conf`

## Limitations

On some systems, the DOSBox window won't consume the whole screen. This might only happen on laptops.

DOSBox's aspect correction is ugly (it just inserts an extra line every 4). hq2x helps a lot with this. You can't use OpenGL scaling on the framebuffer to scale properly.

## Advanced Topics

If you want to do these, I assume you understand a bit about Linux and filesystem images and other stuff. If you're not comfortable with those topics and just want to play DOS games, read no further.

### Copying Games via USB in Linux/Mac (Not Recommended)

I haven't tested this much, I don't know if it's how you should use the persistent filesystem.

`sudo mkdir -p /mnt/dos`

`sudo mount -o loop /path/to/usbdrive/casper-rw /mnt/dos`

`sudo chmod -R ugo+rw /mnt/dos/upper/home/ubuntu/DOS`

Copy games to `/mnt/dos/upper/home/ubuntu/DOS/`

When finished `sudo umount /mnt/dos`

Safely eject the USB drive.

### Copying Games via USB in Windows (Not Recommended)

I haven't tested this much, I don't know if it's how you should use the persistent filesystem.

I don't use Windows so I don't know the exact steps for this, you'll need to figure the details out yourself.

Use [OSFMount](http://www.osforensics.com/tools/mount-disk-images.html) to mount the `casper-rw` file which is on the USB drive.

Copy games to `/upper/home/ubuntu/DOS/` inside that filesystem.

When done, unmount the OSFMount.

Safely eject the USB drive.

### Note About USB Drive Size

The largest file a FAT32 drive can hold is 4 GiB, and the persistent storage is kept within a single file.

This means even if you use a huge USB drive, the most you'll be able to store in the Linux live environment is 4 GiB of changes.

You can extend this space, see: https://askubuntu.com/questions/138356/how-do-i-get-a-live-usb-to-use-a-partition-for-persistence

If you end up with a casper-rw partition, obviously the instructions above to copy games via mounting the casper filesystem image will be different. If you understand enough to partition a disk, you know what you're doing.

----

## To Do List

I'm happy with this document for now.

The End.