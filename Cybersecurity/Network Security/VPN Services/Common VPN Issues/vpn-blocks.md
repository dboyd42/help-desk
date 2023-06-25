# Public WiFi Blocks VPN 

**Author: David Boyd**<br>
**Updated:** 2023-06-24

## VPN connects to their server, but no data is received

### Solution 1

Use a **portable router** and *UPDATE* the **firmware**.

:warning: This doesn't always work.

#### 1.1 Connecting to a Captive Portal via the GL-iNet portable router

1. Disconnect from all other settings: VPN, AdBlocks, etc
1. `Internet` > `Repeater` > (SSID) > `Join`
1. `Admin Panel` > `MORE SETTINGS` > `Custom DNS Server` > *disable* `DNS 
   Rebinding Attack Protection` > `Apply`

#### 1.2 Upgrade the Firmware on the GL-iNet portable router

1. `UPGRADE` > `Upgrade`

#### 1.3 Connect to the VPN

:bulb: This assumes your VPN has already been configured on the router.

1. `VPN` > `OpenVPN Client` > `Connect`

