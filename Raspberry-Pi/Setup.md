# Setting up a Raspberry Pi
This might be the most easy thing ever to do, but you have to do it before doing anything else with a Raspberry Pi. For the sake of complete documentation these are the steps to follow:

1. Download and install the [Raspberry Pi Imager](https://www.raspberrypi.com/software/) 
2. Select the OS using the "Choose OS" button
3. Select the SD card or USB device using the "Choose Storage" button
4. Click "Write" and wait for the image to write to the storage device

There are plenty of ways to write images to external devices, the Raspberry Pi Imager is the most simple way to do it for a Raspberry Pi OS installation. If you would like to use more exotic installations that are not provided by the imager you could download the image yourself. Then simply use tools like Win32DiskImager to write them to the device.

## Setup WiFi
It might be handy to setup the WiFi connection from the get go, without the need to add a monitor and input devices to the Pi. To do this follow these simple steps (I use Powershell in Windows 10):

1. Open a terminal and set the path to the boot directory of the USB device (`cd D:/`)
2. Run this command: `New-Item -Name "wpa_supplicant.conf" -ItemType "file"`. This creates a file with the name wpa_supplicant.conf
3. Open this file in an editor and add the following content to it:

```
country=NL # Your 2-digit country code
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```
4. Insert the correct WiFi information and save the file

## Headless installation (enable SSH)
If you want to use the Pi as a server it comes in handy if the Pi is available without attaching a monitor and input devices. This way you can just power the Pi and access it from your own computer.

1. Open a Powershell terminal and set the path to the boot directory of the USB device (`cd D:'/`)
2. Run this command: `New-Item -Name "ssh" -ItemType "file"`.

The file remains empty, when Raspberry Pi OS finds this file while booting it enables SSH.

## Access the server from your PC
In my opinion the easiest way to access the Pi through SSH on Windows is by downloading and installing [Putty](https://www.putty.org/). You also have to find the local IP address of the Pi. I use my routers user interface to figure that out. 

When you have Putty running just type the local IP of the Pi into the hostname field and click "Open". The terminal will open and ask for a username. The username is by default "pi", the default password is "raspberry". 

## Finishing up

### Update software
The first thing I would recommend is to update the software on the Pi. To do this run the following commands:

1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. When asked if you want to continue type: "Y" or just hit enter

### Update password
It's really important to update the password of the pi user. To do this follow the following steps:

1. If not done already, SSH into the Pi (see previous chapter)
2. Run this command: `sudo raspi-config`
3. Select "System Options"
4. Select "S3 Password"
5. Type a new strong password and type it again

Good stuff, the pi user has a custom password now!

### Update hostname
The next thing I like to do is update the hostname of the Pi. By default the hostname is "raspberrypi". This gets very confusing when you have multiple Pi's running in your network. So I give them a meaningful name to recognize them by. To do so follow these steps:

1. If not done already, SSH into the Pi
2. Open the configuration: `sudo raspi-config` (if not still open from updating the password)
3. Select "System Options"
4. Select "S4 Hostname"
5. Type the new hostname
6. If it asks if you want to reboot say Yes

That's it. If not already done, give it a quick reboot by running: `sudo shutdown -r now` and you are good to go. Happy hacking!