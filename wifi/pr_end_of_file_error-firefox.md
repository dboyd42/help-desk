# How to Fix the PR_END_OF_FILE_ERROR

**Author:** David Boyd<br>
**Date:** 2023-05-11

> Reference: [Kinsta][kinsta]

## Background

The PR_END_OF_FILE_ERROR is a secure connection issue and is a **Firefox
specific** error.

### System SW

|          |                        |
|----------|------------------------|
| OS       | Asahi                  |
| Browser  | Firefox                |
| Wifi     | Captive Portal w/ Code |
| Location | Bennu                  |

## Solution

#### Reset Firefox's SSL Settings

1. Firefox > Settings (Hamburger) >
2. More Troubleshooting Information >
3. `Refresh Firefox`
4. Close all instances of Firefox: `kill -9 $(pidof firefox)`
5. Reopen Firefox and connect to login page/captive portal

:bulb: If you running into an issue of connecting to the captive portal, try:

1. Go to Firefox's [auto detect captive portal][ff-cp-detect]
2. Bennu's Coffee House specfic [deepcoolclear captive portal][dcc-cp]

<!-- Reference Links -->

[kinsta]: https://kinsta.com/knowledgebase/pr-end-of-file-error/
[ff-cp-detect]: http://detectportal.firefox.com/canonical.html
[dcc-cp]: https://login.deepcoolclear.com/BennuPP/index.php?cok=0mupodjp59m2emngmhfi83q2bf&st=6689jn8ot2t88750dgj7syai8y3mti&pda=0&vsc=&ipaddr=172.16.0.184&tod=1232&noc=noc&vlan=
