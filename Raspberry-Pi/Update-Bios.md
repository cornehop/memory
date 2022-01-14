# Updating the bios of the Raspberry Pi
The Raspberry Pi 4 came with some cooling issues. To resolve those issues you can update the bios to the latest version.

Start by updating the software on the Pi:

`sudo apt update && sudo apt upgrade`

Then we install and update the flash tool:

`sudo apt install rpi-eeprom rpi-eeprom-images`

Now you can run the following command: 

`sudo rpi-eeprom-update`

This will tell you if there is an update available. If so you can open the configuration tool by running this command:

`sudo raspi-config`

Then you go to "6 Advanced Options", go to "A7 Bootloader Version" and select "E1 Latest". Now reboot your Pi to apply the update.