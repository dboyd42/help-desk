Admin
=====

Web Interface:
    http://pi.hole/admin
    http://xxx.xxx.xxx.xxx/admin

reset passwd:	$ sudo pihole -a -p
    p:asshole!!

Install log: /etc/pihole

Restarting PiHole
=================

sudo pihole restartdns

Devices
-------

1.) Network > Change Adapter Properties > Ethernet > Properties > Inernet Protocol Verstion 4 (TCP/IP) Properties > Properties
    [+] Use the following DNS server addresses: <Raspberry Pi Static IP address>
    [+] 192.168.1.253

2.) Restart device

PiHole Info
============
CLI:
	https://docs.pi-hole.net/core/pihole-command/

Installation
============
URL OS: https://www.raspberrypi.org/downloads/raspbian/
URL: https://docs.pi-hole.net/main/basic-install/

Raspberry Pi
------------

sudo su
curl -sSL https://install.pi-hole.net | bash

> create static IP address

<Finish Setup>
reboot

YouTube/Google Ads
------------------

nslookup manifest.googlevideo.com
<note return IPs>

sudo vim /etc/hosts
<insert IPv4 address>
<insert IPv6 address>
:wq

sudo pihole restartdns

Debugging
=========

FTL Not Installing
------------------

sudo vim /etc/resolv.conf
nameserver 8.8.8.8
:wq
<if possible>
    pihole -r
<else>
    GOTO reinstall

Additional Options
-------------------

pihole flushdns

