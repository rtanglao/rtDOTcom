---
layout: post
title: "Cannot compile RStudio server on Raspberry Pi 4 8GB RAM Debian 10 Buster"
---
* I tried to follow the directions in [Setting up your own shiny-server / rstudio-server on a Raspberry Pi 3B+](https://community.rstudio.com/t/setting-up-your-own-shiny-server-rstudio-server-on-a-raspberry-pi-3b/18982) but failed
* My theory is that Debian Buster is too new. If I downgrade to Ubuntu Bionic or Debian Stretch 9, then it would probably work since there are dependency scripts for these older operating systems e.g. `install-dependencies-stretch`
* What can I do?  Hack the script to make it work ? I tried that and failed :-)
* Or more likely just wait until somebody else does it or the R Studio folks do it!
* Anyhow I can use R Studio Server on Mac or Windows and just `scp` things over for now.