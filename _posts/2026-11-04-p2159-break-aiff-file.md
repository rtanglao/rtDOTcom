---
layout: post
title: "How to break up an AIFF file into 1 second chunks"
---
* [Draft](https://checkvist.com/p/MVg7Me1Z01Rz7KOTRFjBf1) [created](https://rolandtanglao.com/2025/11/14/p0908-without-link-blogthis-linkless_blog_all_open/): Nov 5, 2026 04:59 (UTC).
```bash
ffmpeg -i input.aif -f segment -segment_time 1 output_%03d.aif
```
- or 0.25 for 1/4 second chunks etc etc :-)
