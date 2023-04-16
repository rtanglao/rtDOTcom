---
layout: post
title: "WSL systemd kluge no longer needed in Windows 11 because systemd is built-in"
---
* The WSL systemd [kluge](https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me#19september2021-systemctl) is no longer needed so **un-install** it. Then, enable systemd by following [Microsoft's instructions](https://devblogs.microsoft.com/commandline/systemd-support-is-now-available-in-wsl/)
tl;dr: add the following lines to `/etc/wsl.conf`
```
[boot]
systemd=true
```
and then `wsl.exe --shutdown` from powershell
and then install `bottle imp`, <https://github.com/arkane-systems/bottle-imp> and then done :-)


### Previously

* September 19, 2021 [19september2021 systemctl](https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me#19september2021-systemctl)  