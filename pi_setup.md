# Set up your pi
[ [Intro](README.md) ] -- [ **Set Up RasPi** ] -- [ [Install Go](go_install.md) ] -- [ [Install Geth](geth_install.md) ] -- [ [Run Geth](geth_run.md) ] -- [ [Updates](raspi_updates.md) ]

-----
## Download and Load Raspbian Disk image onto the microSD card
**Before proceeding to the next step, you first need to decide how you want to access your Pi for the intial setup process.**
1) Access locally. You will need the following thing(s):
    - a display
    - an HDMI cable
    - an ethernet cable (optional, you can also use wifi)
    - a wired mouse or a wireless mouse w/ a receiver
    - a wired keyword or a wireless keyboard (w/ a receiver or bluetooth)
    - a comupter to write the disk image to microSD card with

2) Access remotely (via SSH) aka "headless". You will need the following thing(s):
    - a computer to write the disk image to microSD card with, and to run Secure Shell (SSH) client on
    - assuming the computer has all necessary peripherals i.e. mouse, keyboard
    - an ethernet cable (optional, you can also use wifi)

**For this tutorial, I set up mine locally and used a VNC Viewer to access the Pi remotely from my main PC.**

### 1) Access Locally ###
**Your Raspbery Pi may come with a microSD card with NOOBS preloaded. In such case, simply insert the microSD card into the card slot on your Pi.**
* Download the latest [Raspbian Stretch With Desktop](https://www.raspberrypi.org/downloads/raspbian/) disk image
* Download the latest [Etcher](https://etcher.io/) and install it (for flashing Raspbian disk image to the microSD card)
* Insert the microSD card into the computer (you might need a microSD card adapter for this)
* Start Etcher program, and select the the microSD card you wish to flash the disk image file (either .img or .zip would work) to
* Double check your hard drive selection, then hit "Flash"
![etcher](pics/pi_setup/1.jpg)

Once finished, eject the microSD card and insert it into the Raspberry Pi. Plug in all the peripherals (i.e. display, mouse, keyboard etc.). Finally, plug in the power adapter and wait for the Pi to boot up. If everyting went well, you should be welcomed with the default Raspbian desktop on the screen.

### 2) Access Remotely via SSH ###
* Download the latest [Raspbian Stretch With Lite](https://www.raspberrypi.org/downloads/raspbian/) disk image
* Download the latest [Etcher](https://etcher.io/) and install it (for flashing Raspbian disk image to the microSD card)
* Insert the microSD card into the computer (you might need a microSD card adapter for this)
* Start Etcher program, and select the the microSD card you wish to flash the disk image file (either .img or .zip would work) to
* Double check your hard drive selection, then hit "Flash"



---

Next: [Install Go >>](go_install.md)
