# Reveal WiFi Password via CLI in Linux

> Author: David Boyd<br>
> Date: 2023-04-10

## Method 1: `nmcli` Non-sudo

```bash
# Show current WiFi password
nmcli device wifi show-password

# List all previously connected WiFis' names
nmcli -g NAME connection show

# Show password for NAME in list
nmcli -s connection show <ESSID> | grep psk

# List all WiFis within range
nmcli device wifi
```

## Method 2: Sudo Required

*Note: Was unable to reveal WiFi password in ArchLinux.*

``` bash
# List all previously connectd WiFis
sudo ls /etc/NetworkManager/system-connections

# Show security details for WiFi NAME
sudo cat /etc/NetworkManager/system-connections/"Name of Wifi"
```
