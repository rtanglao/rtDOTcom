---
layout: post
title: "record on instaMic -> plug into Windows -> convert to mp3 with ffmpeg -> upload with website to micro.blog aka how i recorded this one's for pat"
---

## Pontifications

aka how i recorded [this one's for pat](http://roland.micro.blog/2018/08/15/this-ones-for.html)

1. record on [instaMic](https://instamic.io/pages/instamic-support-mobile-app) which only records WAV files
1. plug into Windows computer or mac  using USB (wireless would be better!)
1. convert to mp3 with [ffmpeg](https://ffmpeg.zeranoe.com/builds/)
1. upload with website to micro.blog 

* here's the ffmpeg command to convert WAV to mp3:

```powershell
 C:\Users\rtang\Documents\ffmpeg-20180815-4f8e65c-win64-static\bin\ffmpeg.exe -i D:\IST_0007.wav -f mp
3 hellopat.mp3
```
