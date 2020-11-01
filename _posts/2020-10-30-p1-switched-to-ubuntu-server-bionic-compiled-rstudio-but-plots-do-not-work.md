---
layout: post
title: "Switched from Buster to Ubuntu Server Bionic Beaver 18.04.4 and compiled RStudio Server and it all works except for plots, need type='cairo' and or xvfb-run"
---

* UPDATE: 31October2020, the problem with X11 and shadow graphics device driver was fixed, see the next post:  [Recompiled R 4.0.3 to not use X11 and to use cairo and now png() works without an X11 error and without a shadow graphics error](http://rolandtanglao.com/2020/10/31/p1-recompiled-r-to-use-cairo-and-not-use-x11-and-now-graphics-work-in-r/)        
* Please refer to previous post:  [Cannot compile RStudio server on Raspberry Pi 4 8GB RAM Debian 10 Buster](http://rolandtanglao.com/2020/10/28/p2-cannot-compile-rstudio-server-debian-buster-raspberry-pi4-debian10/)        
* I switched to Ubuntu Server Bionic Beave 18.0.4.4 in order to be able to compile RStudio (Debian Buster is not a supported OS for RStudio as of this writing. But Bionic is!). And it was easy thanks to [Ubuntu-Server-raspi4-unofficial](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial). Thanks James Chambers!!!!!
* First you need to compile SOCI with `CMAKE_CXX_STANDARD` set to `11`
  * `cmake -G "Unix Makefiles" -DWITH_BOOST=ON -DWITH_ORACLE=OFF -DCMAKE_CXX_STANDARD=11`
* Here's how to compile RStudio itself:
  * Follow [Setting up your own shiny-server / rstudio-server on a Raspberry Pi 3B+](https://community.rstudio.com/t/setting-up-your-own-shiny-server-rstudio-server-on-a-raspberry-pi-3b/18982) and do the following extra steps:
  * `cp` libraries to `/usr/lib` from `/usr/local/lib64`
  * set `RSTUDIO_USE_SYSTEM_SOCI` to `ON`; see issue [6533](https://github.com/rstudio/rstudio/issues/6533)
  * `cmake .. -DRSTUDIO_TARGET=Server -DCMAKE_BUILD_TYPE=Release -DRSTUDIO_USE_SYSTEM_SOCI=ON`
  * install libntirpc-dev,  see [build fails if libntirpc-dev is missing #2023](https://github.com/rstudio/rstudio/issues/2023)
* And it's working except that plots don't work in R Studio which is a major loss of functionality, since it's nice to see the plots running on the same machine. Sad face but still hopeful: here is the error message:
```> p
Error in RStudioGD() : 
  Shadow graphics device error: r error 4 (R code execution error)
In addition: Warning message:
In grDevices:::png("/tmp/RtmpY0wRLe/26bdb48e96ab4a4b9ab8e49c79b53183.png",  :
  unable to open connection to X11 display ''  
```
* PNGs also don't work unless you add `type="cairo"` or use `xvfb-run` to run with a Virtual X11 frame buffer. 