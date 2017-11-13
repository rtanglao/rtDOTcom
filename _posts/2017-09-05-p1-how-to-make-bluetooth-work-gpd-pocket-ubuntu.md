---
layout: post
title: "HOW TO: Make bluetooth work on a GPD Pocket running ubuntu"
---

## Pontifications

* Disclaimer: This works for as of Tuesday September 5, 2017 Ubuntu 16 LTS latest on a GPD pocket. This may not work for other or future versions. NO SUPPORT. NO WARRANTY. LEARN LINUX :-) IF YOU DARE. AND IF YOU LIKE YAK SHAVING :-) Otherwise stick to OS X or Windows LOL

from: [https://www.reddit.com/r/GPDPocket/comments/6w169o/ubuntu_version\_no\_bluetooth\_adapters\_found/](https://www.reddit.com/r/GPDPocket/comments/6w169o/ubuntu_version_no_bluetooth_adapters_found/)

* 1\. in udev rules, create a file called ```99-local-bluetooth.rules``` using your favorite text editor e.g. ```vi```:

```bash
cd /etc/udev/rules.d
sudo vi 99-local-bluetooth.rules 
```

where [99-local-bluetooth.rules](https://gist.github.com/rtanglao/bdf4176d190f6b5f1db6a2e915debcd4#file-99-local-bluetooth-rules) is a one line file with the following contents:

```
SUBSYSTEM=="usb", ATTRS{idVendor}=="0000", ATTRS{idProduct}=="0000", RUN+="/bin/sh -c 'modprobe btusb; echo 0000 0000 > /sys/bus/usb/drivers/btusb/new_id'"
```

* 2\. Then reboot. 
* 3\. The bluetooth adapter will magically appear after reboot in Bluetooth settings