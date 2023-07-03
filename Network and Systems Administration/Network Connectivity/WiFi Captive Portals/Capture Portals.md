# How to Fix your Browser's Captive Portal from NOT Working

**Author:** David Boyd<br>
**Updated:** 2023-07-03

## General Troubleshooting Steps

0. Have you tried turning it off and back on again?
1. Check and disconnect any running VPNs.
2. Try a different browser.
    1. I.e. Ungoogled-Chromium, Chromium, Edge, etc.
3. Unassign any manually assigned DNS address in your computer's **Network
   Adapter Settings (IPv4/IPv6).**
4. Clear your browser's cache
    1. `Settings` > `Clear History`
        1. :bulb: Be sure to check *all* history to include the *cache* & etc.
5. Clear your host's DNS cache

## Firefox

### Disenable/Enable Captive Portal Service

#### [ISSUE]: Captive Portal "Success" but "Unable to Connect" website

| Resolved? | :heavy_check_mark: |
|-----------|--------------------|

1. Go to [about:config](about:config)
2. Search for: `captive`
3. Set `networking.captive-portal-service.enabled = false`

## Browser Captive Portal Websites

- [Apple](http://captive.apple.com)
- [Microsoft](http://msftconnecttest.com/)
- [Google](http://connectivitycheck.gstatic.com/generate_204)
- [Firefox](http://detectportal.firefox.com/success.txt)
- [Android (pre-6.0)](http://clients3.google.com/generate_204)

## Additional Information

**Captive Portal**

- Some WAPs (Wi-Fi Access Points) use a technology known as 'Captive Portal'.
Captive portals work by "hijacking" the brower's HTTP request and re-directing
it to the login portal.

**Hijacking Steps:**

1. HTTP redirect
2. IMCP redirect
3. DNS hijacking

:bulb: The **hijacking** doesn't have to be performed by the browser-\-most 
modern devices will automatically run this "captive portal hijacking 
detection" whenever they connect to an open WiFi then pop up a dialog 
allowing your device to go to the captive portal.

