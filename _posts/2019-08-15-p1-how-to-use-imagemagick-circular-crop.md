---

layout: post
title: "HowTo: Circular Crop with ImageMagick"
---

# Pontifications

* See [How can I combine these commands to achieve circular crop in ImageMagick?](https://stackoverflow.com/questions/41959355/how-can-i-combine-these-commands-to-achieve-circular-crop-in-imagemagick)
* Gotta try this with [my Berlin July 2019 photos](https://www.flickr.com/photos/roland/albums/72157709917594396) and then make a collage of these circular crops!

## Code

```bash
convert -size 200x200 xc:Black -fill White -draw 'circle 100 100 100 1' -alpha Copy mask.png

for f in $(ls *.jpg)
do
  convert $f -gravity Center mask.png -compose CopyOpacity -composite -trim ${f}_output.png
done
```

