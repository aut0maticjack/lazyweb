Many people repeat the meme that the Raspberry Pi *requires* a 2.5A power supply but this is not necessarily true.

This page attempts to quantify Raspberry Pi power requirements, then recommend some power supplies.

## Power Requirements

* The SoC (CPU and GPU) draw at most 800mA when active, typically more like 500mA, and less than 100mA when idle.
* The USB controller requires 240mA
* The LEDs require 5mA each
* HDMI output requires 25mA
* The built-in Ethernet requires 2mA
* The Pi 3's built-in Wifi consumes around 20mA when idle
* Unknown to me: Max current requirements of the Pi 3's onboard Wifi and Bluetooth

So far that's about 1.5A at most. From there, the difference comes in the USB peripherals you plug in. The USB specification mandates that a port can supply up to 500mA, so a Pi 2/3 with 4 USB ports could require up to an additional 2A.

Some examples of devices:

* USB keyboard and mouse usually require 50-150mA each, this differs per device
* One USB WiFi adaptor tested required 40mA, others may differ
* A wired XBox 360 controller requires 450mA

You can quantify power requirements of any specific device you have with `lsusb -v` and the `MaxPower` property.

The following example shows the power requirements for a couple of game controllers:

~~~
$ lsusb -v | egrep "idVendor|idProduct|MaxPower"

  idVendor           0x046d Logitech, Inc.
  idProduct          0xc21f F710 Wireless Gamepad [XInput Mode]
    MaxPower               98mA

  idVendor           0x0738 Mad Catz, Inc.
  idProduct          0x3187 
    MaxPower              500mA
~~~

References:

* https://www.raspberrypi.org/help/faqs/#powerReqs
* https://en.wikipedia.org/wiki/Raspberry_Pi#Specifications
* http://www.jeffgeerling.com/blogs/jeff-geerling/raspberry-pi-zero-power
* http://www.jeffgeerling.com/blogs/jeff-geerling/raspberry-pi-zero-conserve-energy
* http://www.pidramble.com/wiki/benchmarks/power-consumption

## Power Supplies

**Don't use cheap rubbishy power supplies!!!**

If you're seeing the small rainbow square in the top right corner, your Raspberry Pi is not getting enough power. Specifically, power has dropped to 4.65V or less.

Note this is *not* the giant rainbow splash screen which appears on boot. That's the GPU self-test and is perfectly normal. If desired, you can disable the rainbow splash screen with `disable_splash=1` in `/boot/config.txt`.

If you're seeing the yellow/orange/red square in the top right corner, those are temperature warnings.

There are many aspects to a good power supply, covered in great detail on [Ken Shirrif's blog](http://www.righto.com/2012/10/a-dozen-usb-chargers-in-lab-apple-is.html).

I have used iPad chargers exclusively since I discovered Ken's blog, and have almost never seen the rainbow under-voltage square. You can get them in stores everywhere for under AUD$30.

It's true that the iPad charger does sag voltage at max load, but with my usages all being under 2A I'm happy I'm getting enough power.

It's true that HP and Samsung chargers are better, but they are hard to find in stores, and I don't trust eBay sellers enough that I believe they're genuine items and not inferior clones.

Other good choices are probably the [Adafruit Power Supply](https://www.adafruit.com/product/1995) and the [Official Raspberry Pi Power Supply](https://www.raspberrypi.org/products/universal-power-supply/).

The USB cable you're using matters as well. I've had cheap USB cables which could barely carry 200mA. Monoprice and BlitzWolf are good brands for USB cables. Fast-charge cables which come with brand-name smartphones and tablets are probably a good choice too.

You'll always get some voltage drop over a USB cable, a typical 1 metre cable drops about 0.25V. Some power supplies (like Adafruit) make up for this by intentionally supplying 5.25V. A very long cable like 3 metre or more is probably unsuitable to power a Raspberry Pi.

The Raspberry Pi 2 and Raspberry Pi 3 are said to be less sensitive to lower voltage and voltage fluctuations than the Raspberry Pi 1. 

References:

* http://www.righto.com/2012/10/a-dozen-usb-chargers-in-lab-apple-is.html
* https://www.raspberrypi.org/forums/viewtopic.php?t=82373