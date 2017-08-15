# dflyfwconf

DragonFly BSD Firewall Configuration

These config files are examples. At least `rc.conf` needs some changes for your system. Compare with the originals carefully.

The `rc.conf` file has two openvpn configs, disabled. See `CHANGEME` in the file, and see your original `rc.conf` for values. DO NOT USE THE VALUE WITH `CHANGEME` IN THEM. They are there just to remind you that my `rc.conf` has those values set, for completeness.

The `pf.conf` file has rules enabling openvpn. Comment those out if you aren't using openvpn. I currently do not have rules that filter the openvpn traffic to certain hosts. You will probably want to do that for security. I also have allowed `ssh` and `http` access. Comment those out if you desire.

The `dhcpd.conf` file needs to be copied to `/usr/local/etc/dhcpd/`, after you do `pkg install dhcpd` or otherwise install it from ports. This file, combined with the config in `rc.conf` and `pf.conf` sets up a DHCP network on 192.168.2.1 on your second network device. You may need to change the network to avoid conflicting with work or other VPN'd networks. It also has the nameserver pushed to clients set to 8.8.8.8 which are google's servers. Change this as you see fit.

If you are using openvpn, you need to create the openvpn config files somehow, and change the `rc.conf` `openvpn*_configfile` variables to the path of each config file.

If you are using `tunnelblick` on a Mac, then it will have the OpenVPN files that you can copy in place. Your system administrator might have them generated for you already. You need to `pkg install openvpn` or otherwise install it from ports.

On boot, and periodically, after openvpn connection fails, I often need to do `rcrestart pf` and/or `rcrestart openvpn` in a certain combination or order, to get the VPN back online. Try playing with OpenVPN config settings for keep alive, and/or having a tmux window open on the other side which updates the clock in the terminal window, to keep the connections going. The AWS VPN seems to not need that very often, but my work VPN seems to need it often. 

