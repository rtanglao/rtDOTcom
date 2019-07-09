---
layout: post
title: "To plot geom_density() using the colours from your data you need a colour vector and scale_colour_manual"
---

## Pontifications

* To plot ```geom_density()``` using the colours from your data instead of R's colour palettes  you need a [named colour vector](http://rolandtanglao.com/2016/08/01/p1-howto-named-character-vector/) (see ```A:``` in the code below) as well as [a mapping in your geom](http://rolandtanglao.com/2017/08/07/p4-part4-ig-van-jan2016-colour-the-dots-with-the-right-colour-name/) i.e. ```geom_density()``` for ```aes``` colour (see ```B:```) and ```scale_colour_manual()``` (see ```C:```). Not sure why you need the ```scale_colour_manual()``` to be honest!

Here's the code:

```R
# A:
# Don't need as.character() since it's already a character
colour_named_vector <- setNames
(singleton_colours_removed_average_colour_ig_van_jan2016_with_colourname$colourname, singleton_colours_removed_average_colour_ig_van_jan2016_with_colourname$colourname)

ggplot(
singleton_colours_removed_average_colour_ig_van_jan2016_with_colourname, 
aes(x=colourname))+
geom_density(mapping = aes(colour= colour_named_vector))+ # B:
scale_colour_manual(values=colour_named_vector) #C:
```

Output:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36102051403/in/datetaken/" title="ggplot(singleton_colours_removed_average_colour_ig_van_jan2016_with_colourname, aes(x&#x3D;colourname))+geom_density(mapping &#x3D; aes(colour&#x3D; colour_named_vector))+scale_colour_manual(values&#x3D;colour_named_vector)"><img src="https://farm5.staticflickr.com/4386/36102051403_c74879ce2d_n.jpg" width="320" height="221" alt="ggplot(singleton_colours_removed_average_colour_ig_van_jan2016_with_colourname, aes(x&#x3D;colourname))+geom_density(mapping &#x3D; aes(colour&#x3D; colour_named_vector))+scale_colour_manual(values&#x3D;colour_named_vector)"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>