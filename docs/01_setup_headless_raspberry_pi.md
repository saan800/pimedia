# Setup Raspberry Pi with headless access

You don't need a monitor, screen or tv to be able to use your Raspberry Pi. You can easily setup headless access using your laptop to directly access the Pi.

## Setup SD Card

* Insert SD Card into laptop
* [Download Raspberry Pi Imager and install Raspberry Pi OS on SD Card](https://www.raspberrypi.org/downloads/)
  * Raspberry Pi OS Lite (32 bit)
    * uses less CPU and memory, faster to create images and boot Pi
    * only have access to the command line (no GUI desktop)
  * Raspberry Pi OS (32 bit)
    * **PREFERRED FOR PIMEDIA BUILD:** if you want GUI desktop
  * Raspberry Pi OS Full (32 bit)
    * if you want GUI desktop with all RPi apps installed
* You'll probably need to remove SD Card and re-plug into laptop for next steps
* Enable headless access
  * [Enable wifi](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md) (optional)
    * This step is unnecessary if the Pi will be connected via LAN cable instead of wifi.
    * Add `wpa_supplicant.conf` file to the root directory. 
    The below config worked for me in UK.
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=GB

network={
 ssid="YOUR_WIFI_NAME"
 psk="YOUR_WIFI_PASSWORD"
}
```
  * [Enable ssh](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)
    * Add empty file named `ssh` to root directory
* Eject SD card from laptop and insert into Pi
* Power on Raspberry Pi and give it a few minutes to startup
  * Lights on Pi will stop flashing when finished the install
  * Should not need to be connected to monitor/TV, but it can be useful to see whats going on

## Update Raspberry Pi via command line

* Open up the command line on the Pi
  * [Connect to Raspberry Pi from laptop](02_connect_to_raspberry_pi_from_laptop.md)
  * Connect a physical screen and keyboard attached to the Pi
* The first time you connect to the Pi you will be prompted to change the password password, by a message like the following
  * `SSH is enabled and the default password for the 'pi' user has not been changed. This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.`. 
* Lets fix that and create a more secure user login

```
pi@raspberrypi:~ $ sudo passwd pi
New password: 
Retype new password: 
passwd: password updated successfully
```

Ensure everything is up to date

```
sudo apt update
sudo apt full-upgrade -y
sudo apt-get update
sudo rpi-update
sudo reboot
```

Give the Pi a few minutes to shutdown and restart.

## Thanks to

* https://medium.com/coinmonks/run-raspberry-pi-in-a-true-headless-state-cfb3431667de

[Back to index](index.md)
