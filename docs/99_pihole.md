# PiHole in OMV

## Setup VLAN

* Login to [Portainer](http://pimedia:9000/)
  * Go to `Images`
  * From `DockerHub` pull the image `pihole/pihole`

<img src="img/99_pull_pihole__docker_image.png" />

* In OMV
  * Go to `System` > `Network` and the `Interfaces` tab
  * Select `eth0` and edit
    * Set `DNS Servers` to `1.1.1.1`
* Open Pi command line via ssh

```
docker network create -d macvlan --subnet=192.168.1.10/24 --gateway=192.168.1.1 -o parent=eth0 pub_net
```




## More details

* [How to install Pi-hole on OpenMediaVault 5 using Docker with Portainer on Raspberry Pi 4](https://www.youtube.com/watch?v=sEHXzR7fOo8&list=PLulABMF2ltKoQFbhWSZpvhQx9KXXMibKa&index=25)
* https://pcmac.biz/pi-hole-on-openmediavault-5-inside-docker-with-portainer-using-raspberry-pi-4/