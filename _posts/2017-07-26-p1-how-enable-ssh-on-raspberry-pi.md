---
layout: post
title: "How to enable ssh on raspbian on a Raspberry PI"
---

## Pontifications

* From [ssh Raspberry pi tutorial](https://www.raspberrypi.org/documentation/remote-access/ssh/) via [ssh connection refused on Raspberry Pi on Stack Overflow](https://stackoverflow.com/questions/41318597/ssh-connection-refused-on-raspberry-pi):

**QUOTE**

"As of the November 2016 release, Raspbian has the SSH server disabled by default. It can be enabled manually from the desktop:

1.  Launch Raspberry Pi Configuration from the Preferences menu
2.  Navigate to the Interfaces tab
3.  Select Enabled next to SSH
4.  Click OK

Alternatively, raspi-config can be used:

1. Enter sudo raspi-config in a terminal window
2. Select Interfacing Options
3. Navigate to and select SSH Choose Yes
4. Select Ok
5. Choose Finish

### Enable SSH on a headless Raspberry Pi
For headless setup, SSH can be enabled by placing a file named ssh, without an extension, onto the boot partition of the SD card. When the Pi boots, it looks
for the ssh file. If it is found, SSH is enabled, and the file is deleted. The
content of the file does not matter: it could contain text, or nothing at all."

**END QUOTE**