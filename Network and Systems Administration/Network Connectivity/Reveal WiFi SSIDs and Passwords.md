# Reveal WiFi Password via CLI 

> Author: David Boyd<br>
> Updated: 2023-07-03
>> Creation Date: 2023-04-10

## Linux

### Method 1: `nmcli` Non-sudo

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

### Method 2: Sudo Required

*Note: Was unable to reveal WiFi password in ArchLinux.*

``` bash
# List all previously connectd WiFis
sudo ls /etc/NetworkManager/system-connections

# Show security details for WiFi NAME
sudo cat /etc/NetworkManager/system-connections/"Name of Wifi"
```

## macOS

### Method 1: CLI

- :computer: Regardless of prepending `sudo`, you'll need to input your Mac's
admin username and password in the pop-up prompt.

``` bash
security find-generic-password -ga <SSID> | grep "password:"
```

### Method 2: GUI

1. Open **Keychain Access:**
    1. `C-Space` (Spotlight Search) 
    2. Input "`Keychain Access`" 
2. In **Keychain Access:** 
    1. Click `Local Items` in the left column
    2. Search for the SSID in the top centered search bar w/ the magnifying
       glass
    3. Open the WiFi's profile by double-clicking on the SSID
    4. Click on the `[] Show password:` checkbox
    5. Input your Mac's admin username and password in the pop-up prompt

