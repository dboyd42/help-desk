# How to Configure X11 Forwarding Run GUI Apps Using SSH

**Author:** David Boyd<br>
**Date:** 2023-07-23

## Table of Contents

- [Introduction](#introduction)
- [Objective](#objective)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Step 1: Router Setup](#step-1-router-setup)
  - [Step 2: Kali Linux Setup](#step-2-kali-linux-setup)
  - [Step 3: macOS Setup](#step-3-macos-setup)
  - [Step 4: Let the Magic Begin...](#step-4-let-the-magic-begin)
- [Tips and Best Practices](#tips-and-best-practices)

## Introduction

One thing that bugs me about Mac is their non-compatability of their Aarch64
chips with x86_x64.  So this guide will show you how I was able to setup an SSH
connection with pseudo-GUI (X11 port forwarding) on an M1 MacBook Pro.


## Objective

Securely access my Kali x64 virtual machine that resides on my Proxmox home
server over the interwebs.

To get this machine:

| Specs |                |
|-------|----------------|
| Chip  | Apple M1       |
| macOS | Ventura 13.2.1 |

To connect to this machine:

| Specs |                   |
|-------|-------------------|
| Chip  | Intel x86_x64     |
| Linux | 6.3.0-kali1-amd64 |

## Prerequisites

Although I did this at coffee shop using a VPN, I'd highly recommend that you'd
have physical access to both machines AND your router.

## Steps

- [Port Forwarding Setup](#port-forwarding-setup)
- [Statically Assign Kali VM IP Address](#statically-assign-kali-vm-ip-address)

#### Step 1: Router Setup 

#### Port Forwarding Setup

This exact steps will be dependent upon your router, but generally they follow
the same steps:

1. Login to your router's admin page
2. Go to `Firewall` > `Virtual Servers / Port Forwarding`
3. Add a Virtual Server with similar settings:

| Setting            | Value                           | Setting | Value   |
|--------------------|---------------------------------|---------|---------|
| Description        | Port Forward to Proxmox Kali VM |         |         |
| Inbound Port       | `12345`                         | to      | `12345` |
| Format             | Both                            |         |         |
| Private IP Address | `10.0.0.2`                      |         |         |
| Local Port         | `12345`                         | to      | `12345` |

- :bulb: Of course you'd choose something randomly ephermal for your ports!

A reboot ought not to be required, but it doesn't hurt to go ahead and do this.

#### Statically Assign Kali VM IP Address

The purpose of statically assigning your Kali VM an IP address is so the
previous step will be persistent with forwarding the traffic to your machine.

1. Login to your router's admin page.
2. Go to `LAN Setup` > `Client List`
3. Copy the **MAC Address** under **Attached Client List** section.
4. Click `Add` Reserved IP Client and input the similar settings:

| Settings    | Value                      |
|-------------|----------------------------|
| Name        | Kali-VM                    |
| IP Address  | 10.0.0.2                   |
| MAC Address | [paste what you've copied] |

5. Click `Add Client` then `Apply`

### Step 2: Kali Linux Setup

1. Set up your statically assigned IP in the `/etc/network/interfaces` file:

``` bash
# Proxmox interface (not pfSense)
auto eth0
iface eth0 inet static
  address 10.0.0.2
  netmask 255.255.255.0
  gateway 10.0.0.1
  broadcast 10.0.0.255
  dns-nameservers 1.1.1.1, 1.0.0.1
```

- :bulb: The DNS nameservers aren't necessary.

2. Replace the following values for the settings below in our
`/etc/ssh/sshd_config`:


``` bash
Port 12345
PasswordAuthentication no
PermitRootLogin no
MaxStartups 3
MaxAuthTries 3
X11Forwarding yes
```

:bulb: You may want to hold out on `PasswordAuthentication no` until everything
else is setup as SSH key issue(s) are not addressed in this guide.

3. Ensure the following programs are installed:

``` bash
# XAuth
which xauth

# SSH
systemctl status ssh
# If not enabled/running:
systemctl enable --now ssh
```

### Step 3: macOS Setup

1. Ensure that [XQuartz][xquartz-official] is installed:

``` bash
which xquartz
```

If not, download it from [XQuartz official site][xquartz-official] and follow
the guided instructions then **REBOOT YOUR MACBOOK**
:exclamation::exclamation::exclamation:

- :bulb: I installed this Xquartz from the website albeit the existence of
Xquartz being already installed. Luckily, no conflicts or errors occurred, but
this may have aided in the setup and proceeding steps.

2. Allow XQuartz to allows connections from the client to open an X11
   window on your Mac:

    - Open **X11 Preferences** `XQuartz` > `Settings` > `Security`:
      -  [X] Allow connections from network clients

3. Verify the following binary exists:

``` bash
ls /opt/X11/bin/xauth
```

4. Configure your `~/.ssh/config` file:

``` bash
Host whateverName-Kali
    HostName my.public.ip.address       # Go online & get your public IP addr
    User kali
    Port 12345                          # Make it ephemeral!
    XAuthLocation /opt/X11/bin/xauth
    ForwardX11Trusted yes
    ForwardX11 yes
```

### Step 4: Let the Magic Begin...

1. Open an SSH connection with X11 port forwarding enabled:

``` bash
ssh -X whateverName-Kali
```

2. Once connected, open a GUI app from the commandline:

``` bash
sudo apt install geany -y
geany
```

After a few moments, Geany (a lightweight note taking app) will appear in an
X11 window you macOS.  Woot woot!

## Tips and Best Practices

:warning: Be careful as this opens up a port on the internet that anyone can
see.  Don't believe me, check out Shodan and if its a Well-Known port, then
they'll for sure have it listed within a few weeks. So far, they haven't
obtained any of my ephemeral ports. For example, they showed SSH port 22
open--but unbeknownst to them it was my honeypot, lol.

:warning: Would also recommend to setup SSH key authentication if you haven't
already. No one should be accessing your machine with just a password.
DigitalOcean's [How To Configure a SSH Key-Based Authentication on a Linux
Server][do-sshauth] is a great write-up on how to set this up.

<!-- Reference Links -->

[do-sshauth]: https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server
[xquartz-official]: https://www.xquartz.org/

