---
layout: post
title: "SoftCreatR's Imagemagick Easy install for Ubuntu and Debian aka 'imei' worked for me on my Raspberry Pi 400 running Debian bullseye"
---
*  [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): Feb 5, 2023. 00:31 SoftCreatR's [imei](https://github.com/SoftCreatR/imei/) aka `Imagemagick easy install` fixed my jpeg delegate issues on debian bullseye running on a Raspberry Pi 400. Found via Stack Overflow: [What is simplest process to get ImageMagick 7 with PNG support](https://askubuntu.com/questions/1216469/what-is-simplest-process-to-get-imagemagick-7-with-png-support-on-ubuntu). I just followed the [One Step Automated Install](https://github.com/SoftCreatR/imei/#one-step-automated-install), namely:
```bash
t=$(mktemp) && \
wget 'https://dist.1-2.dev/imei.sh' -qO "$t" && \
bash "$t" && \
rm "$t"
```
### Previously
* April 26, 2021 [How To install Imagemagick on Ubuntu 20.04 with JPG, PNG and TIFF support aka 'delegates'? Why isn't this in the default install?](http://rolandtanglao.com/2021/04/26/p1-how-to-install-imagemagick-ubuntu-2004-jpeg-png-tiff-delegates/) <-- This didn't work for me on my Rapsberry Pi 400 running Debian bullseye in 2023!