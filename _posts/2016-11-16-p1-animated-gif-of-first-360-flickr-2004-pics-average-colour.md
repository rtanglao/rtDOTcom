---
layout: post
title: Animated GIF of first 360 photos average colour flickr 2004
---

Following on from [yesterday's thrilling post :-)](http://rolandtanglao.com/2016/11/15/p1-compositing-only-works-with-transparent-pngs/) 

## Pontifications


* Here are the magic commands ([full details](https://github.com/rtanglao/rt-animated-gifs#november-15-2016)) to make the animated gif:<br /> 

```sh 
ls -1 000*.png >roland-1st360-flickr-average-colour.txt
./convert-create-composite-gifs-from-file-list.rb roland-1st360-flickr-average-colour.txt
gm convert -loop 50 -delay 10 -scale 256x256 convert-composite*.png convert-composite256-first360-flickr-roland-2004-12-avgcolour.gif
```

* Why ```-scale 256x256``` ? To limit the file size to 256 so it can fit in Twitter's 15MB limit
* [Pomax](http://pomax.github.io/) writes: [neat! can you make the edges opacity-faded so it blends?](https://twitter.com/TheRealPomax/status/798768593575952385) Anybody know how to do that in imagemagick? If so email me: roland at rolandtanglao.com or tweet @rtanglao

### Animated GIF output

![animated gif first 360 average color's of roland's flickr 2004](https://c2.staticflickr.com/6/5529/31006323266_e4674046ca_o_d.gif)