# Set up your pi
[ [Intro](README.md) ] -- [ **Set Up RasPi** ] -- [ [Install Go](go_install.md) ] -- [ [Install Geth](geth_install.md) ] -- [ [Run Geth](geth_run.md) ] -- [ [FAQ](faq.md) ] -- [ [Updates](raspi_updates.md) ]

-----
## Remarks regarding using the command line
- Every command in this guide starts with a $ sign. You don't actually have to type the $ sign into the command line.
- While using the Nano text editor, press `ctrl+o`then`Enter`to save or `ctrl+x` to exit.
- To read more on Linux command line, check out this [article](https://www.computerworld.com/article/2598082/linux/linux-linux-command-line-cheat-sheet.html)
## Download and load Raspbian disk image; Establish connection to the Pi
**Before proceeding to the next step, you first need to decide how you want to access your Pi for the intial setup process.**
1) Access locally. You will need the following thing(s):
    - a display
    - an HDMI cable
    - an ethernet cable (optional, you can also use wifi)
    - a wired mouse or a wireless mouse w/ a receiver
    - a wired keyword or a wireless keyboard (w/ a receiver or bluetooth)
    - a comupter to write the disk image to microSD card with
    - an external hard drive for storing blockchain data (ideally 500GB+)

2) Access remotely (via SSH) aka "headless". You will need the following thing(s):
    - a computer to write the disk image to microSD card with, and to run Secure Shell (SSH) client on
    - assuming the computer has all necessary peripherals i.e. mouse, keyboard
    - an ethernet cable (optional, you can also use wifi)
    - an external hard drive for storing blockchain data (ideally 500GB+)

**For this tutorial, I set up mine locally and used a VNC Viewer to access the Pi remotely from my main PC.**

### 1) Access Locally ###
**Your Raspbery Pi may come with a microSD card with NOOBS preloaded. In such case, simply insert the microSD card into the card slot on your Pi.**
* Download the latest [Raspbian Stretch With Desktop](https://www.raspberrypi.org/downloads/raspbian/) disk image
* Download the latest [Etcher](https://etcher.io/) and install it (for flashing Raspbian disk image to the microSD card)
* Insert the microSD card into the computer (you might need a microSD card adapter for this)
* Start Etcher program, and select the the microSD card you wish to flash the disk image file (either .img or .zip would work) to
* Double check your hard drive selection, then hit "Flash"

![etcher](pics/pi_setup/1.jpg)

Once finished, eject the microSD card and insert it into the Raspberry Pi. Plug in all the peripherals (i.e. display, mouse, keyboard etc.). Finally, plug in the power adapter and wait for the Pi to boot up. If everyting went well, you should be welcomed with the default Raspbian desktop on the screen. You can now go ahead and set up wifi connection etc.

### 2) Access Remotely via SSH ###
* Download the latest [Raspbian Stretch With Lite](https://www.raspberrypi.org/downloads/raspbian/) disk image
* Download the latest [Etcher](https://etcher.io/) and install it (for flashing Raspbian disk image to the microSD card)
* Insert the microSD card into the computer (you might need a microSD card adapter for this)
* Start Etcher program, and select the the microSD card you wish to flash the disk image file (either .img or .zip would work) to
* Double check your hard drive selection, then hit "Flash"

**Now we need to establish SSH connection on the Pi**
* Go to the root directory of the microSD card, and creat an empty file named `ssh` without a file extension. This will automatically enable ssh upon booting up.
* Connect an ethernet cable to the Pi. If you wish to use wifi connection instead, create a file named `wpa_supplicant.conf` in the root directory of the microSD card, and write the following content:
```
country=US
ctrl_interface=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="SSID"
    psk="passwrod"
}
```
**Replace `US` with the ISO Alpha-2 code of the country you are located in. You can look it up [here](http://www.nationsonline.org/oneworld/country_code_list.htm).**
**Also replace `SSID` and `password` with your own wifi credentials**

Once finished, eject the microSD card and insert it into the Raspberry Pi. Plug in the power adapter and wait for the Pi to boot up. If everyting went well, you should see one red led light staying on and one green led light flashing steadily.

Next, we want to assign the Pi a static IP address so that we don't have to constantly change it for future SSH logins.
* Access your router by following this [guide](https://wiki.amahi.org/index.php/Find_Your_Gateway_IP)
* Find the corresponding menu for assigning static IP addresses
* Change the last part of the Pi's IP address to any number in the range of 0-255 (e.g. `24` for pi_4) 
![router](pics/pi_setup/2.png)

Lastly, we need to run an SSH client to remotely access the Pi with. Personlly I use [PuTTY](edgebase/finding-your-default-gateway/) on Windows. If you use Mac OS or Linux, first you will need to open up Terminal. Run `$ ssh pi@ip_address` and hit Return key when finished. When asked for password, enter `raspberry` and you will be in.

![ssh1](pics/pi_setup/ssh1.jpg)
![ssh2](pics/pi_setup/ssh2.jpg)

To test the internet connection on the Pi, run `$ ping cypher-core.com` in terminal. If you see pings, that means it's working.

![ping](pics/pi_setup/ping.jpg)

## Configure the Pi
**Here are a few settings you can configure to optimized the Pi for our use.**
- Change user password
- Change Host name
- Manage network connections
- Update configuration tools
- Boot options 
    * -> Desktop / CLI -> CLI
    * -> wait for network to boot
- Localisation
- Overclock
- Advanced options 
    * -> Expand Filesystem
    * -> set Memory Split to `16`

To access these menus, simply go to `Preferences -> Raspberry Pi Configuration` if you are accessing the Pi via a display.

![config1](pics/pi_setup/config1.jpg) ![config2](pics/pi_setup/config2.jpg)

If you are running the Pi "headless", type in `$ sudo raspi-config`.

![config3](pics/pi_setup/config3.jpg)

## Mount external hard drive; Move "swap file"
For this step, you can use either a pre-formatted hard drive or an existing hard hard that contains data. If you need to format an existing hard drive, use any tool you prefer just make sure you format it with **NTFS**. Once the hard drive is ready, simply plug it into the pi.

- Identify the partition; install NTFS dependency 
<br/>`$ lsblk -o UUID,NAME,FSTYPE,SIZE,LABEL,MODEL`
<br/>`$ sudo apt-get install ntfs-3g`
<br/>![1](pics/hdd_mount/1.jpg)
<br/> Here I'm using the `sda2` partition

- Edit the `fstab` file
<br/>~ open up the file: `$ sudo nano /etc/fstab`
<br/>~ add this line at the end of the file:`UUID=[YOUR_UUID] /mnt/hdd ntfs defaults,auto,umask=002,gid=pi,users,rw 0 0`
<br/>![2](pics/hdd_mount/2.jpg)

- Create a directory for the hard drive
<br/>`$ sudo mkdir /mnt/hdd`

- Check if `/mnt/hdd` is correctly mounted
<br/>`$ sudo mount -a`
<br/>`$ df /mnt/hdd`
<br/>![3](pics/hdd_mount/3.jpg)

- Set the owner of `/mnt/hdd`
<br/>`$ sudo chown -R pi:pi /mnt/hdd/`

- Creat a directory for Ethereum blockchain data
<br/>`$ cd /mnt/hdd/`
<br/>`$ mkdir eth_data`
<br/>`$ ls -la`
<br/>![7](pics/hdd_mount/7.jpg)

- Go back to `/home/pi`
<br/>`$ cd`

SD card failure is a common issue people encounter in projects. To prevent that, we can move the "swap file" onto an external drive so that the SD card doesn't degrade too quickly.

- Edit the "swap file"
<br/>~ open up the file: `$ sudo nano /etc/dphys-swapfile`
<br/>~ modify the following lines as shown:
<br/>`CONF_SWAPFILE=/mnt/hdd/swapfile`
<br/>`CONF_SWAPSIZE=1000`
<br/>![4](pics/hdd_mount/4.jpg)

- Delete old "swap file", and enable the new one
<br/>`$ sudo dphys-swapfile swapoff`
<br/>`$ sudo rm /var/swap`
<br/>`$ sudo dphys-swapfile setup`
<br/>`$ sudo dphys-swapfile swapon`
<br/>![6](pics/hdd_mount/6.jpg)

---

Next: [Install Go >>](go_install.md)
