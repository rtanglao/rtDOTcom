---
layout: post
title: ggplot2&#58; aes MAPS geom SETS
---

## Why does the following R program using ggplot2 work?
Answer: because aes MAPS values and geom SETS values!

    getnumericColour <-
    function(colorname) {
    colour_matrix=col2rgb(colorname)
    return(as.numeric(colour_matrix[1,1]) * 65536 +
    as.numeric(colour_matrix[2,1]) * 256 +
    as.numeric(colour_matrix[3,1]))
    }
    color_ints_all = sapply(sorted$colorname,getnumericColour)
    colour_hex_strings_all = sapply(color_ints_all, function(x){
    sprintf(“#%6.6X”, x)})
    ggplot(sorted,aes(x=colorname,y=count))+
    geom_bar(colour=colour_hex_strings_all,
    stat=“identity”,fill=colour_hex_strings_all)+
    scale_x_discrete(limits = sorted$colorname)+
    scale_fill_manual(values = colour_hex_strings_all)
