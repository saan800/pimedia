# Boot from USB drive

SD cards were never intended for fast read-write access. Attaching a SSD drive via USB 3.0 port can [provide a dramatic increase to performance](https://www.tomshardware.com/uk/news/raspberry-pi-4-ssd-test,39811.html). The Raspberry Pi 4 B comes with two USB 3.0 ports.

## Hardware

You need some form of USB storage
* SSD/HDD to USB 3.0 enclusure
  * https://www.amazon.co.uk/gp/product/B07VXF2HJG
    * has its own power supply so more reliable/longer lasting SSD/HDD functionality
  * USB C enclosure
    * USB A 3.0 -> USB C can get up to 6 (10?) Gbps transfer rate
    * https://www.amazon.co.uk/gp/product/B07D2BHVBD
    * https://www.amazon.co.uk/gp/product/B07RZBTNTN
    * https://www.amazon.co.uk/gp/product/B07ZDRCQPG
  * Or even a Raspberry Pi 4 case with built in SSD/HDD expansion
    * https://thepihut.com/products/argon-one-m-2-raspberry-pi-4-case
    * https://thepihut.com/products/retroflag-nespi-4-case-for-raspberry-pi-4
* A compatible SSD/HDD drive to fit the enclosure
* Standard Portable USB drive (not recommended)
  * Its possible to setup with a USB flash drive, but apparently it does not perform well


## Ensure you can connect to drive from the Pi

### Raspberry Pi 4 requires recent boot EEPROM

* Check [Raspberry Pi 4 boot EEPROM](https://www.raspberrypi.org/documentation/hardware/raspberrypi/booteeprom.md) version
  * From SSH command line run `rpi-eeprom-update` to check if you need to update it

<img src="img/03_verify_eeprom_version.PNG" />


## Enable USB mass storage boot

### Using `raspi-config`

* Connet to Pi command line via SSH (details in [Setup Raspberry Pi with headless access](01_setup_headless_raspberry_pi.md))
* Run `sudo raspi-config`
* Choose `Advanced Options`

<img src="img/03_boot_options.PNG" />

* Choose `Boot order`

<img src="img/03_boot_order.PNG" />

* Choose `USB Boot`
* Exit the `raspi-config` screen
* Shutdown the Pi from command line: `sudo halt` ?? TODO: or sudo shutdown?
* Disconnect power
* Remove SD Card from Pi

## Booting from the USB mass storage device

* Connect SSD/HDD drive to laptop via USB
* Ensure drive is empty - formatting for Pi will erase all files
* Follow the steps from [Setup Raspberry Pi with headless access > Setup SD Card](01_setup_headless_raspberry_pi.md#setup-sd-card), except do for drive instead of SD Card
  * Use the same OS version that you did for the SD Card
  * Remember to do the "Enable headless access" steps too
* Eject drive from laptop
* Ensure Raspbery Pi is still powered down from previous step
* Connect drive to USB 3.0 port on the Raspberry Pi
* Start the Pi
  * Depending on the size of the drive, this could take a while
  * May need to repeat [Find Raspberry Pi's IP Address](https://github.com/saan800/pimedia/blob/main/docs/02_connect_to_raspberry_pi_from_laptop.md#find-raspberry-pis-ip-address) steps

## More details

* https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md
* https://www.raspberrypi.org/documentation/configuration/raspi-config.md
* https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711_bootloader_config.md
* https://www.raspberrypi.org/documentation/configuration/raspi-config.md

[Back to index](index.md)


maybe
* https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md
* https://www.raspberrypi-spy.co.uk/2014/05/how-to-mount-a-usb-flash-disk-on-the-raspberry-pi/
* https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711_bootloader_config.md
* https://www.raspberrypi.org/documentation/hardware/raspberrypi/booteeprom.md 
* https://www.makeuseof.com/tag/connect-hdd-raspberry-pi/
* https://www.easeus.com/storage-media-recovery/usb-external-hard-drive-shows-up-in-device-manager-but-not-in-this-pc.html#part1