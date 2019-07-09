---
layout: post
title: How to make a bar graph from a CSV file using colours in the CSV file itself
---

R is horrible :-) but powerful and you don’t need for loops almost never! (the type system is horrible, the error messages are horrible, etc)

Copying from a [github gist](https://gist.github.com/rtanglao/e0a183170ac2710cb5ef) (which are also horrible since github will eventually turn e*il and destroy all our gists):

    sorted = read.csv(“/Users/rolandtanglao/Dropbox/PHOTOS/instagram-top10-vancouver-2014/sorted-ig-van-2014-top-colour-names.csv”)
    counts3 = head(sorted[,2],200)
    colours3 = head(sorted[,1],200)
    barplot(counts3, main=“Colour Distribution”,
    col=colours3,
    xlab=“Top Colours”,
    ylab=“Colour Counts”)



