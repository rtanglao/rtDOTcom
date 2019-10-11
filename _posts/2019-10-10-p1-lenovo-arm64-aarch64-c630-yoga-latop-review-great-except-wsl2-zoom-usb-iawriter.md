---

layout: post
title: "Anecdotal review of Lenovo C630 Yoga ARM64 / AARCH 64 Windows 10 laptop: great except for WSL2 not working, USB not working with Zoom"
---

# Pontifications

* I've had the [Lenovo C630 Yoga ARM64 / AARCH 64 Windows 10 laptop since June 1, 2019](http://rolandtanglao.com/2019/05/30/p1-hello-world-from-arm64-windows-lenovo-c630-yoga/).
* It's great; great battery life, Firefox nightly AARCH64 works well, but there are quirks that might be showstoppers for you.
  * USB is flakey; it doesn't work well in Zoom (not sure Zoom supports ARM64 fully)
  * [WSL 2 doesn't work](http://rolandtanglao.com/2019/09/15/p3-wsl2-does-not-work-on-arm64-because-you-cannot-enable-the-hypervisor-in-the-bios/) (it works on some ARM 64 laptops like the Samsung Galaxy Book 2)
  * [IA Writer doesn't work with WSL files](http://rolandtanglao.com/2019/07/08/p1-ia-writer-01july2019-build-still-hangs-when-opening-wsl-files/) (I use Typora  instead) . To be fair it doesn't work for x64 either!
  * x86 32 bit printer drivers don't work on AARCH64. At least [the 32 bit driver for the Ricoh MP2504EX doesn't work](https://twitter.com/rtanglao/status/1182381981251686400).

