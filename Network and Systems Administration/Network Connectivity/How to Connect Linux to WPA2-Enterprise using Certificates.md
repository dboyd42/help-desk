# Connect Linux to WPA2-Enterprise with User and CA Certificates

**Author:** David Boyd<br>
**Date:** 2024-04-20

## Table of Contents

<!-- vim-markdown-toc GFM -->

* [Overview](#overview)
* [Step 1: Download Certificates](#step-1-download-certificates)
* [Step 2: Configuration](#step-2-configuration)
  * [Plasma KDE](#plasma-kde)
    * [Connections: Wi-Fi](#connections-wi-fi)
    * [Connections: Wi-Fi Security](#connections-wi-fi-security)

<!-- vim-markdown-toc -->

## Overview

Network certificates are often used in colleges and enterprises to connect to
their WiFi.

## Step 1: Download Certificates

0. Conect to the WiFi
1. Download:
    * CA certificate 
      * `*.cer` (default) or `*.pem`, `*.der`
    * User certificate
      * `*.p12` (default) or `*.pfx`, `*.pem`, `*.pvk`

## Step 2: Configuration

### Plasma KDE

1. Connect to the secure WiFi
2. **Connections - System Settings** configuration:

#### Connections: Wi-Fi

|             Setting | Value                            | *(Data Type)* |
|--------------------:|:---------------------------------|--------------:|
|               SSID: | \<secure-wifi-name>              |    *(string)* |
|               Mode: | Infrastructure                   | *(drop-down)* |
|              BSSID: | \<blank>                         |      *(null)* |
| Restrict to Device: | \<blank>                         |      *(null)* |
| Cloned MAC Address: | \<blank>                         |      *(null)* |
|                MTU: | \<blank>                         |      *(null)* |
|        Visisbility: | [ ] *(Unchecked)* Hidden network |      *(null)* |

#### Connections: Wi-Fi Security 

|                      Setting | Value                                             | *(Data Type)* |
|-----------------------------:|:--------------------------------------------------|--------------:|
|                    Security: | WPA/WPA2 Enterprise                               | *(drop-down)* |
|              Authentication: | TLS                                               | *(drop-down)* |
|                    Identity: | \<Username>                                       |    *(string)* |
|                      Domain: | \<blank>                                          |      *(null)* |
|            User certificate: | \<Client Certificate `*.p12`>                     |      *(file)* |
|              CA certificate: | \<Root CA Certificate `*.cer`>                    |      *(file)* |
|               Subject match: | \<blank>                                          |      *(null)* |
| Alternative subject matches: | \<blank>                                          |      *(null)* |
|    Connect to these servers: | \<blank>                                          |      *(null)* |
|                 Private key: | \<Client Certificate `*.p12`>                     |      *(file)* |
|        Private key password: | \<Same as when prompted to download certificates> |    *(string)* |


<!-- References -->
