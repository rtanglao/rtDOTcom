---
layout: post
title: "Use hugo server --renderToDisk to force your Hugo posts to be rendered to disk instead of RAM which is the current default"
---

# Pontifications

* Use `--renderToDisk` or there will be nothing rendered. i.e. no HTML web pages just cached versions in RAM.  [renderToDisk](https://kodify.net/hugo/config/command-flags-options/) doesn't seem be much slower then rendering to RAM!

* The full command line to run the local server is:

```bash
hugo server --buildDrafts --disableFastRender --renderToDisk &
```
* See [How I created RollingRoland.com using hugo, hover.com DNS and surge.sh](http://rolandtanglao.com/2016/10/28/p1-how-i-made-rollingroland/) which referred to an earlier version of Hugo that didn't require `renderToDisk`