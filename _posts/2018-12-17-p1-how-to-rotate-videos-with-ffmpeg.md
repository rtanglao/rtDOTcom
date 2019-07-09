---
layout: post
title: "How to rotate videos with ffmpeg"
---
## Pontifications

* Usually it's just the metadata!
* from [SO:Rotating videos with FFmpeg](https://stackoverflow.com/questions/3937387/rotating-videos-with-ffmpeg), here's how to change the metadata from 90 to 0

```bash

ffmpeg -i ~/Downloads/45620789954.mp4 -map_metadata 0 -metadata:s:v rotate="0" -codec copy 16dec2018-cypress-powerline-xc-rotated.mp4 # preserves metadata

```