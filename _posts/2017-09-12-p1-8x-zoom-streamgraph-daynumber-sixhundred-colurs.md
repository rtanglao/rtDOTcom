---
layout: post
title: "8x zoom option to webshot - R - streamgraph of instagram vancouver january 2016 average colour by 600 plotrix integer colours on y axis, x axis is jan 1,2,3,...31"
---

## Pontifications

* Same as yesterday with 8x [zoom](https://www.rdocumentation.org/packages/webshot/versions/0.4.1) using ```webshot```
* Critical code (marked with "A)" )is:

```R
html_print(
    streamgraph( groupedby_date_sixhundred_colourint,
                "sixhundred_colourint", "n", "date",
                interactive=FALSE) %>% 
    sg_fill_manual(values=colour_named_vector),
    viewer = NULL
) %>%
    normalizePath(.,winslash="/") %>%
    gsub(x=.,pattern = ":/",replacement="://") %>%
    paste0("file:///",.) %>%
    webshot(
        file = "8x-zoom-artofwhere-headless-streamgraph.png", delay = 10,
        selector = ".streamgraph",
        zoom = 8 # A) https://www.rdocumentation.org/packages/webshot/versions/0.4.1
        )  
}
```

## 800% zoom of Streamgraph of 600 int colours of string Colourname : average colour instagram vancouver january 2016 aes-x-hour-y-colourname* Invoked as:

```bash
cd /Users/rtanglao/Dropbox/GIT/2016-r-rtgram/JANUARY2016
Rscript ../leggings-artofwhere-streamgraph-600colour-int-ig-van-jan2016-avgcolour.R
```


Code:  [https://github.com/rtanglao/2016-r-rtgram/blob/master/leggings-artofwhere-streamgraph-600colour-int-ig-van-jan2016-avgcolour.R](https://github.com/rtanglao/2016-r-rtgram/blob/master/leggings-artofwhere-streamgraph-600colour-int-ig-van-jan2016-avgcolour.R)



### Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/36384524243/in/datetaken-public/" title="8x-zoom-artofwhere-headless-streamgraph"><img src="https://farm5.staticflickr.com/4403/36384524243_2fe7038f2c.jpg" width="500" height="260" alt="8x-zoom-artofwhere-headless-streamgraph"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>