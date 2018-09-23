---
layout: post
title: "Launching Windows Firefox from WSL works, just set the BROWSER environment variable"
---

## Pontifications

* I was wrong when I wrote: [Still can't launch Firefox from Windows Subystem From Linux without a Selenium server and some hacks that nobody has working (Chrome works though)](http://rolandtanglao.com/2018/09/09/p1-still-cannot-launch-firefox-from-wsl-without-lots-of-yakshaving/) back on September 9, 2018.
* It's easy to use the ```Launchy``` ruby gem
* Just set the ```BROWSER``` enviroment variable and the Launchy just works:

```bash
export BROWSER='/mnt/c/Program\ Files/Mozilla\ Firefox/firefox.exe'
```