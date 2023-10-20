# How to Remote into Computer using VNC over SSH

**Author:** David Boyd<br>
**Date:** 2023-10-20

## Table of Contents

<!-- vim-markdown-toc GFM -->

* [Cheat Sheet (Post-Installation)](#cheat-sheet-post-installation)
  * [1. Start VNC on server](#1-start-vnc-on-server)
  * [2. Establish SSH tunnel then connect on client](#2-establish-ssh-tunnel-then-connect-on-client)
* [Introduction](#introduction)
* [Objective](#objective)
* [Prerequisites](#prerequisites)
* [Steps](#steps)
  * [Step 1: Set Up the Server (Linux)](#step-1-set-up-the-server-linux)
    * [1.1: Install the VNC Server](#11-install-the-vnc-server)
    * [1.2: Make the Binary Accessible to the Local User](#12-make-the-binary-accessible-to-the-local-user)
    * [1.2: Set Up a VNC Password](#12-set-up-a-vnc-password)
    * [1.3: Start the VNC Server](#13-start-the-vnc-server)
  * [Step 2: Set Up the Client (MacBook)](#step-2-set-up-the-client-macbook)
    * [Step 2.1: Install the VNC Viewer Client](#step-21-install-the-vnc-viewer-client)
    * [Step 2.2: Establish an SSH Tunnel and Forward the VNC Port](#step-22-establish-an-ssh-tunnel-and-forward-the-vnc-port)
      * [Optional: Pre-Configure SSH for X-Forwarding and Security](#optional-pre-configure-ssh-for-x-forwarding-and-security)
* [Tips and Best Practices](#tips-and-best-practices)
  * [SSH and Port Forwarding](#ssh-and-port-forwarding)
  * [Proxmox Hypervisor Environment](#proxmox-hypervisor-environment)
* [Troubleshooting](#troubleshooting)
  * [Computer is Running but Can't Connect](#computer-is-running-but-cant-connect)
  * [Computer is Running but Session is Frozen](#computer-is-running-but-session-is-frozen)
    * [Bind [127.0.0.1]:5901: Address already in use](#bind-1270015901-address-already-in-use)
  * [X Connection to :1 Broken](#x-connection-to-1-broken)
    * [Option 1: Restart the VNC server on the Server Machine](#option-1-restart-the-vnc-server-on-the-server-machine)
    * [Option 2: Check for Port Conflicts](#option-2-check-for-port-conflicts)
  * [Can't Locate the VNC Password File](#cant-locate-the-vnc-password-file)

<!-- vim-markdown-toc -->

## Cheat Sheet (Post-Installation)

### 1. Start VNC on server

``` bash
vncviewer :1 -geometry 1280x720
```

### 2. Establish SSH tunnel then connect on client

``` bash
# Replace `my-comp` with assigned name
ssh -NTf -L 5901:localhost:5901 my-comp && remote-viewer vnc://localhost:5901
```

## Introduction

As I've enjoyed SPICE (Simple Protocol for Independent Computing Environments),
for remote desktop, multiple issues become apparent when attempting to access a
VM from Proxmox via a CloudFlare tunnel (over the Internet) AND when
attempting to bypass the that tunnel which results in both high latency and
insecure connections. Using VNC over SSH provides a lower latency and secure
conenctions (granted that you change the SSH defaults to something more
secure).

This setup uses the following nodes and software:

| Component     | Spec       | Additional Info             |
|---------------|------------|-----------------------------|
| the server    | Kali VM    | Runs in a PVE               |
| the client    | macOS      | Sonoma 14.1 Beta (23B5067a) |
| tigervnc      | VNC server |                             |
| remote-viewer | VNC client |                             |

:bulb: The following contains commands relative to a Debian-based distro,
modify any commands to fit whichever distro you are running.

## Objective

The following steps sets up a VNC (Virtual Network Computing) desktop protocol
to connect securely over the Internet via SSH.

## Prerequisites

1. Update the server (the remote computer we're connecting to)

- Debian-based: `sudo apt update -y`
- Arch-based: `sudo pacman -Syu` (:warning: `--no confirm` is NOT recommended!)

2. The client (the local computer connecting to the server)

- macOS:

``` bash
# Install Homebrew (you should already have it if you're reading this!)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew update
``````

## Steps

### Step 1: Set Up the Server (Linux)

VNC (Virtual Network Computing) is a protocol (a technology) used for remote
desktop access and virtualiztion. VNC allows you to control a remote computer's
desktop over a network. We'll be implementing VNC through the TigerVNC Project
which will give us access to the `vncserver` program. The `vncserver` CLI
allows us to start and manage VNC server sessions on our Linux machine.

#### 1.1: Install the VNC Server

``` bash
sudo apt install tigervnc-common tigervnc-standalone-server -y
```

#### 1.2: Make the Binary Accessible to the Local User

:warning: This is a SECURITY RISK and I don't recommend you run this in a
production environment.

The reason behind this is to make sure that the client logs into the local
user; else the client logs into the root user by default. This most likely
happens because `vncserver` requires us to run sudo, and by doing so, we
inevitably establish a VNC server with `root` user. To combat this, we'll
remove the `sudo` requirments to the `vncserver` binary for *the* local user.

``` bash
# Create/Append a Sudoers file to enable NOPASSWD for vncserver command
sudo echo "<username> ALL=NOPASSWD:/usr/bin/vncserver" >> /etc/sudoers.d/<username>
```

Next, you'll have to logout and log back in. But as I tend have multiple
connections, I suggest a reboot as it'll cover all your bases.

#### 1.2: Set Up a VNC Password

This password will be the same one that the user enters in their VNC client
when establishing an initial connection to the remote computer.

``` bash
vncpasswd
```

:bulb: `sudo` should not be required if the previous step worked.

:bulb: This password is persistent as it's saved to an encrypted file:
`~/.vnc/passwd`. However, feel free to change it by re-running the `vncpasswd`
command.

#### 1.3: Start the VNC Server

Start the VNC server, specifying the display number and geometry (resolution)
as desired. Replace <display-number> with your chosen display number (e.g., 1)
and <width>x<height> with your preferred screen resolution.

``` bash
# SYNTAX
vncserver :<display-number> -geometry <width>x<height>
```

``` bash
vncserver :1 -geometry 1280x720
```

:eyes: Note the VNC Server IP Address and Port:

- To access your VNC server over the Internet, you'll need to know the IP
  address of your Debian-based computer.
- Note the port number used by your VNC server (typically `5900` + display
  number). For display 1, it would be 5901.

### Step 2: Set Up the Client (MacBook)

#### Step 2.1: Install the VNC Viewer Client

There a multiple choices from `remote-viewer`, **RealVNC**, **TightVNC**,
**Chicken of the VNC (macOS)**, **Vinagre**, **NoMachine**, and even
**Microsoft Remote Desktop (RDP)**. But as I'm coming from Virt-Viewer
background, I'm all about dem `remote-viewer` apps. Anyways, let's get to it!

``` bash
brew install virt-viewer
```

#### Step 2.2: Establish an SSH Tunnel and Forward the VNC Port

With our server running the VNC server, and our client having the viewer
software, we're now ready to connect to our remote computer!

``` bash
# 1. Establish an SSH tunnel to remote machine
ssh -NTf -L 5901:localhost:5901 server-username server-ip 

# 2. Connect to remote machine via SSH tunnel 
remote-viewer vnc://localhost:5901
```

| Flag | Description                                                  |
|------|--------------------------------------------------------------|
| `-N` | Do not execute a remote command (used when forwarding ports) |
| `-T` | Disable pseudo-tty allocation (else no GUI)                  |
| `-f` | Send `ssh` to background (else VNC password is inaccessible) |
| `-L` | `-L`ink the addresses: `[bind_address:]port:host:hostport`   |


##### Optional: Pre-Configure SSH for X-Forwarding and Security

Although this guide doesn't fully talk about SSH security, this following
configuration will save you time in so that you only need to run a Bash
one-liner from your client (where `my-comp` is the remote-computer).

``` bash
ssh -NTf -L 5901:localhost:5901 my-comp && remote-viewer vnc://localhost:5901
```

## Tips and Best Practices

### SSH and Port Forwarding

With SSH, it's best to use public key access only and to change the port
number to some randomly riduculous ephermeral number ESPECIALLY because this VM
will be opened on the world wide interwebs.

- But to do this, you'll need to set up port forwarding on your router as well.
This is simply to mitigate those bots from attempting access on your machine.
If you've ever looked over a honey pot's logs, you'll know exactly what I'm
talking about!

### Proxmox Hypervisor Environment

Don't openly run your PVE's web interface on the Internet without considerable
protections.

## Troubleshooting

1. Check the VNC Log for Errors: `cat /home/user/.vnc/sub.domain.com:1.log`

### Computer is Running but Can't Connect

You may need to log into the server first. You can access the server by
either logging into the PVE's (Proxmox Virtual Environment) web interface or by
SSH (if previously configured).

### Computer is Running but Session is Frozen

Unfortunately, when the server logs you out due to idle time, the session also
freezes. You can re-establish the session from the client `ssh -NTf -L
5901:localhost:5901 server-username server-ip && remote-viewer
vnc://localhost:5901`.

An alternative proactively *insecure* solution would be to turn off or increase
the max logout time. :warning: I would suggest this only if you plan to
shutdown the when you are done for the day.

#### Bind [127.0.0.1]:5901: Address already in use

The issue is pretty self explanatory, but it ultimately means that there's
already a background process (or connection) in use; and your client is keeping
that route connection alive even though the end point ends in a dead end.

If the following error occurs on the client machine:

``` bash
bind [127.0.0.1]:5901: Address already in use
channel_setup_fwd_listener_tcpip: cannot listen to port: 5901
Could not request local forwarding.
```

Then identify and the stop the process using port 5901:

1. Find the process using port 5901: `lsof -i :5901`
2. Kill the found PID: `kill <PID>`

Or run the following Bash one-liner:
- `lsof -i :5901 | tail -n1 | cut -d ' ' -f6 | xargs -I _ kill _`

### X Connection to :1 Broken

If you recieve a similar error:

``` bash
=================== tail /home/someUser/.vnc/sub.domain.com:1.log ===================
[mi] mieq: warning: overriding existing handler (nil) with 0x557718b1a180 for event 2
[mi] mieq: warning: overriding existing handler (nil) with 0x557718b1a180 for event 3
X connection to :1 broken (explicit kill or server shutdown).

Mon Oct  9 16:10:42 2023
 ComparingUpdateTracker: 0 pixels in / 0 pixels out
 ComparingUpdateTracker: (1:-nan ratio)
Killing Xtigervnc process ID 12844... success!
=======================================================================================
```

#### Option 1: Restart the VNC server on the Server Machine

``` bash
# 1. List the running VNC servers
vncserver -list

# 2. Kill them all! (Replace :1 with the correct display number)
vncserver -kill :1

# 3. Start a new VNC server session
vncserver :1 -geometry 1280x720
```

#### Option 2: Check for Port Conflicts

``` bash
# Find listening TCP ports
sudo netstat -tulnp | grep 5901

# Kill them all! ... maybe
sudo kill <PID>

# 3. Start a new VNC server session
vncserver :1 -geometry 1280x720
```

### Can't Locate the VNC Password File

If you recieve a similar error:

``` bash
Mon Oct  9 16:08:05 2023
 vncext:      VNC extension running!
 vncext:      Listening for VNC connections on local interface(s), port 5901
 vncext:      created VNC server for screen 0
3NI3X0 New Xtigervnc server 'sub.domain.com:1 (<username>)' on port 5901 for display :1.
3NI3X0 Use xtigervncviewer -SecurityTypes VncAuth -passwd /tmp/tigervnc.zfHNjO/passwd :1 to connect to the VNC server.
[mi] mieq: warning: overriding existing handler (nil) with 0x5650a1683180 for event 2
[mi] mieq: warning: overriding existing handler (nil) with 0x5650a1683180 for event 3
X connection to :1 broken (explicit kill or server shutdown).

Mon Oct  9 16:08:07 2023
 ComparingUpdateTracker: 0 pixels in / 0 pixels out
 ComparingUpdateTracker: (1:-nan ratio)
Killing Xtigervnc process ID 11153... success!
```

Then either create the missing directory and password file:

``` bash
# 1. Locate the password file FROM THE ERROR MESSAGE
cd /tmp
ls -alh tigervnc.zfHNjO/  # If it exists
ls -alh tigervnc.zfHNjO/passwd  # If it exists

# 2. Create the missing directory and/or passwd
mkdir -p /tmp/tigervnc.zfHNjO
touch /tmp/tigervnc.zfHNjO/passwd

# 3. Set the proper permissions
chmod 600 /tmp/tigervnc.zfHNjO/passwd

# 4. Restart the VNC server
vncserver -list
vncserver -kill :1
vncserver :1 -geometry 1280x720
```

And then reconnect to the server from the client device.

:thinking: Another alternative may to just re-run `vncpasswd` then restart the
VNC server. Haven't tried this though #food-for-thought

<!-- Reference Links -->

