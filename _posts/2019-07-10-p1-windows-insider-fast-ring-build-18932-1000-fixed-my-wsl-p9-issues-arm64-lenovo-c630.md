---

layout: post
title: "Windows Insider Fast Ring Build 18932.1000 fixed my issues accessing \\\\wsl$ as well as running explorer.exe on Lenovo Yoga C630 ARM64. Thanks to WSL issue 4016"
---

# Pontifications

* I googled my dmesg error message on my ARM64 Lenovo C630:

```
[0.453819] <3>init: (1) ERROR: LogException:23:\
FS: Could not start file system server. Invalid argument @.\plan9.cpp:88 (CreateServerSocket)
```

* This led me to: WSL issue 4016 which is reported on the exact same hardware:   [init: LogException:23 FS: Could not start file system server #4016](https://github.com/microsoft/WSL/issues/4016)  where I found out that [brion](https://github.com/brion) had solved the issue by: ```For me, it cleared up after upgrading to the Fast ring build 18917; file server seems to work ok there.```
* So, I upgraded to  the most bleeding edge Windows 10 build: Windows Insider Fast Ring Build 18932.1000 and voila all the bugs were fixed! I can now access ```\\wsl$\``` and ```explorer.exe .``` from WSL works i.e. the bug is fixed that I complained about back on May 30, 2019 [Accessing WSL files from File Explorer using  \\\wsl$\Ubuntu appears to be broken in ARM64 Windows 10 Builds on Windows  10 Build 1903](http://rolandtanglao.com/2019/05/30/p2-accessing-wsl-files-from-file-explorer-using-wsl-file-explorer-arm64-windows10-build-1903/)
* Hooray, this means I can use my C630 for all of my Mozilla work that involve WSL!!!!! Very big win!
