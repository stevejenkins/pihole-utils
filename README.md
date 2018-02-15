# pihole6check - Pi-hole IPv6 config updater
A script that checks the Pi-hole server's current IPv6 address and updates the IPv6 address configured in ```/etc/pihole/setupVars.conf``` if necessary.

# Why pihole6check?
If your ISP changes your IPv6 Global Unicast Address, Pi-hole becomes misconfigured and times out when trying to load a page. Running pihole6check fixes the issue... at least until your ISP changes your IPv6 address again.

# Requirements
pihole6check requires that you have <a target="_blank" href="https://github.com/pi-hole/pi-hole">Pi-hole</a> running on your system.

# Usage
1. Clone or download the ```pihole6check``` directory to your host's `/usr/local/bin/` directory.
2. Run ```/usr/local/bin/pihole6check/pihole6check``` from the command line.

Once you're satisfied with pihole6check's performance, set an hourly cron job to run ```pihole6check``` like this:

    @hourly /usr/local/bin/pihole6check/pihole6check > /dev/null 2>&1 #Check Pi-hole IPv6 configuration
    
# Credits
* Original version of the script written by *linuxpng* in <a target="_blank" href="https://discourse.pi-hole.net/t/some-websites-load-very-slow/1876/46">this thread</a> on the Pi-hole support forums.