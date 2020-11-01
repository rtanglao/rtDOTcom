---
layout: post
title: "Recompiled R 4.0.3 to not use X11 and to use cairo and now png() works without an X11 error and without a shadow graphics error"
---

* Please refer to previous post:  [Switched  from Buster to Ubuntu Server Bionic Beaver and compiled RStudio Server  and it all works except for plots, need type='cairo' and or xvfb-run](http://rolandtanglao.com/2020/10/30/p1-switched-to-ubuntu-server-bionic-compiled-rstudio-but-plots-do-not-work/)            

* Recompiled R 4.0.3 to not use X11 and to use cairo and now png() works without an X11 error and without a "shadow device graphics error".  Here's the  `configure` command which I discovered from [straychild01's comment](https://community.rstudio.com/t/setting-up-your-own-shiny-server-rstudio-server-on-a-raspberry-pi-3b/18982/39) on [Setting up your own shiny-server / rstudio-server on a Raspberry Pi 3B+ ](https://community.rstudio.com/t/setting-up-your-own-shiny-server-rstudio-server-on-a-raspberry-pi-3b/18982) on the R Studio Community Forum

```bash
./configure --with-x=no --with-cairo=yes --with-libpng=yes --enable-R-shlib`
```

* This also means `xvfb-run` is not required to start up RStudio server.