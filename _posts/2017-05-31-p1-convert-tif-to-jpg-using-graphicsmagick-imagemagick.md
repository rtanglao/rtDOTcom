---
layout: post
title: How to convert all TIFFs to PNGs in a separate sub directory using ImageMagick / GraphicsMagick
---

## Pontifications
From [stack overflow Batch Processing tif images? Converting .tif to .jpeg](https://askubuntu.com/questions/60401/batch-processing-tif-images-converting-tif-to-jpeg), I modified ```jpg``` to be ```png```. This uses ```imagemagick``` but I believe if you add ```gm``` in front of convert you can use ```graphicsmagick```

```bash
mkdir PNG; convert *.TIF -set filename: "%t" PNG/%[filename:].png
```