# Overclocking the Raspberry Pi
To get the maximum out of your Pi you can decide to overclock the CPU. Ofcourse there is some downsides to this. The Pi will get significantly warmer, so you should apply some cooling to it to protect it from overheating.

## Update the firmware
First we want to make sure the firmware running on the Pi is the most recent version. This can be achieved by the running following commands:

`sudo apt update`
`sudo apt full-upgrade`

Then reboot to apply the updates:

`sudo reboot`

## Inspect the current CPU values
Now we would like to display the current CPU values, this can be done with the following command:

`lscpu`

This displays the values like displayed below:

```
Architecture:        armv7l
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  1
Core(s) per socket:  4
Socket(s):           1
Vendor ID:           ARM
Model:               3
Model name:          Cortex-A72
Stepping:            r0p3
CPU max MHz:         1500.0000
CPU min MHz:         600.0000
BogoMIPS:            108.00
Flags:               half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
```

Right here you can see that the maximum CPU speed is 1500 MHz (1.5GHz).

## Update the config file
To overclock the Pi we have to edit the config.txt file. To open this file in the CLI editor (nano):

`sudo nano /boot/config.txt`

Add the bottom of the file we want to add the following lines:

```
# CPU overclocking
over_voltage=6
arm_freq=2000
```

Now just reboot the Pi and check with `lscpu` if the max. speed is 2000 MHz. I've read online that you can even overclock higher by setting `arm_freq=2147` and `gpu_freq=750`. But in my case the Pi would not boot with those settings.