---
layout: post
title: "How to turn off Windows Defender for Windows Subystem for Linux from @leandrw"
---

## Pontifications

* Turn off Windows Defender for Windows Subystem for Linux to speed up your command line scripting! It's at least twice as fast!
* From [@leandrw: Speeding up WSL I/O up than 5x fast + saving a lot of battery life & CPU usage](https://medium.com/@leandrw/speeding-up-wsl-i-o-up-than-5x-fast-saving-a-lot-of-battery-life-cpu-usage-c3537dd03c74):

**QUOTE**

<blockquote>
So, to do so, first get the UbuntuOnLinux (or your distro of choice) installation path going to <i>%USERPROFILE%\AppData\Local\Packages</i> and lookup for something like :<br ><b>CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc.</b><br /><br />

Copy the entire path from Explorer.exe address bar, then go to <br /><i>Settings > Update & Security > Windows Defender > Open Windows Defender Security Central > Protection Against Viruses & Threats > Advanced Config… > Exclusions > Add or Remove > Add > Folder</i> and finally: paste the previous copied path

</blockquote>

**END QUOTE**

```



