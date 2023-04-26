# Linux networking cheat sheet


## setting up address
addresses are set up by editing yaml files in `/etc/netplan/` , while making sure that correct interface is configured. Yaml files are case sensitive and space sensitive.
wifis is configured same as eth with exception of adding ssid and password of connection
`hostname` used to check and set new hostname 

## ping
`ping <dst>` "pings keeps pinging untill stopped"
`ping -c <number> <dst>` "specifies how many packets to send"
`mtr <domain>` sends pings and shows live traceroute

## interfaces
`ifconfig` "shows interfaces"
`iwconfig`
`ip`  "latest and updated version of ifconfig"
`ifup <interface>` "enable interface"
`ifdown <interface>` "disable interface"
`ifplugstatus` checks if interfaces are plugged in

## traceroute
`traceroute <dst>` "shows names and devices on path, follows route to dst, should report where network latency comes from" 
`traceroute -n <dst>` "avoids reverse DNS lookup"
`sudo traceroute -I <dst>` specifies ICMP`-I` or TCP `-T` packets (UDP by default)
`tracepath <dst>` "similar to traceroute"
`mtr <domain>` sends pings and shows live traceroute

## traffic
`iftop` traffic monitoring on interface, must be ran as sudo, `-B` to get data in bytes
`sudo iftop -I <interface>`
`sudo iftom -P`
`tcpdump` packet capture tool

## ?
`netstat` "?" "used with `-p -s -r`"
`ss` "alternative for netstat"

`dig <domain name> ` "outputs records (A by default), specify `dig <domain name> MX` or NX or ANY", 
`nslookup <domain name>` "older version of dig" basically shows ipv4 and ipv6 of domain

`route` displays routing table, 
`route add default gw <IP>` to add addressto routing table
`arp` shows arp table
`whois` shows 'all' information of a webiste
