---
layout: post
title: Two ways to get Average Colour Using ImageMagick convert command
---


## Pontifications

### 1 Scaling to 1x1


```sh
convert rose: -scale 1x1 \
-format '%[fx:int(255*r+.5)],%[fx:int(255*g+.5)],%[fx:int(255*b+.5)]'\
info:-
```

### Output

```sh
146,89,80
```

### 2 Histogram

```sh
convert rose:  -fordepth 8  histogram:info:- | sort -r | head
```

### Output

```sh
21: (255,255,255) #FFFFFF white
14: (254,254,252) #FEFEFC srgb(254,254,252)
10: (104,101, 86) #686556 srgb(104,101,86)
 9: (105, 96, 81) #696051 srgb(105,96,81)
 7: (108, 99, 84) #6C6354 srgb(108,99,84)
 6: (107, 98, 83) #6B6253 srgb(107,98,83)
 6: (105, 98, 82) #696252 srgb(105,98,82)
 5: (255,255,254) #FFFFFE srgb(255,255,254)
 5: (105,102, 87) #696657 srgb(105,102,87)
 5: (104, 99, 83) #686353 srgb(104,99,83)
```

