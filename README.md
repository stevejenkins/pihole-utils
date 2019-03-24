# pihole-utils - A Growing Collection of Utilities for the Pi-hole Ad Blocker
This repo contains a collection of helper scripts I use in conjunction with the popular [Pi-hole](https://pi-hole.net/) ad blocking server. For more info visit the Pi-hole [website](https://pi-hole.net/) or [GitHub repo](https://github.com/pi-hole/pi-hole).

## Installing the pihole-utils Collection
You can download the latest stable version of these Pi-hole helper scripts directly to your Raspberry Pi (or to any other Linux-based Pi-hole server) directly from GitHub. If you don't already have ```git``` installed on your system, do:

```sudo apt-get update && sudo apt-get -y install git```

then install the ```pihole-utils``` collection with:

```sudo git clone https://github.com/stevejenkins/pihole-utils.git```

Please feel free to improve these scripts and/or submit your own Pi-hole helper scripts for inclusion in this repo.

## pihole_static_sort - Sorts the Pi-hole Static DHCP Lease File
A script that sorts the DHCP static lease file (```/etc/dnsmasq.d/04-pihole-static-dhcp.conf```) by IP address for easier manual editing and verification. If this file is misconfigured or contains duplicates, dnsmasq won't start and Pi-hole won't issue DHCP addresses. The ability to visually scan through a sorted file is helpful when troubleshooting... and also makes those of us with OCD tendencies breathe easier when we cat the file. :)

I plan on adding command-line options in a future version that allow a choice of whether to sort by MAC address, IP address, or hostname. But for now, if you're familiar with the Linux ```sort``` command, you can edit the appropriate line of the script to make the ```sort``` command do what you want before it writes the sorted file back to the ```/etc/dnsmasq.d``` directory.

### Requirements
```pihole_static_sort``` requires that you have <a target="_blank" href="https://github.com/pi-hole/pi-hole">Pi-hole</a> running on your system.

### Usage
1. Clone or download the ```pihole-utils``` repo to your host's `/usr/local/bin/` directory.
2. Run ```/usr/local/bin/pihole-utils/pihole_static_sort``` from the command line.

## pihole_ipv6_check - Pi-hole IPv6 Configuration Updater
A script that checks the Pi-hole server's current IPv6 address, compares it to the IPv6 address configured in ```/etc/pihole/setupVars.conf```, then updates the configuration if necessary.

### Why pihole_ipv6_check?
If your ISP changes your Pi-hole host's IPv6 Global Unicast Address, Pi-hole becomes misconfigured and your clients will time out when trying to load certain pages. Running ```pihole_ipv6_check``` fixes the issue... at least until your ISP changes your IPv6 address again!

More info about what causes certain Pi-hole slowdowns can be found here:

https://pi-hole.net/2018/02/02/why-some-pages-load-slow-when-using-pi-hole-and-how-to-fix-it/

### Requirements
```pihole_ip6_check``` requires that you have <a target="_blank" href="https://github.com/pi-hole/pi-hole">Pi-hole</a> running on your system.

### Usage
1. Clone or download the ```pihole-utils``` repor to your host's `/usr/local/bin/` directory.
2. Run ```/usr/local/bin/pihole-utils/pihole_ipv6_check``` from the command line.

Once you're satisfied with pihole_ipv6_check's performance, set an hourly cron job for the ```root``` user to run ```pihole_ipv6_check``` like this:

    @hourly /usr/local/bin/pihole-utils/pihole_ipv6_check > /dev/null 2>&1 #Check Pi-hole IPv6 configuration
    
### Credits
* Original version of the IPv6 address-checking script written by *linuxpng* in <a target="_blank" href="https://discourse.pi-hole.net/t/some-websites-load-very-slow/1876/46">this thread</a> on the Pi-hole support forums.
