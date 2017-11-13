---
layout: post
title: ggplot2&#58; working histogram plot with labels
---

Working R code with labels ([pdf file of the graphic](https://www.dropbox.com/s/pn3wnnxbdwm8xos/ig-vancouver-2014-topcolour-all-ggplot2-Rplot46.pdf?dl=0)):

    ggplot(sorted,aes(x=colorname,y=count))+
    geom_bar(colour=colour_hex_strings_all,  
    stat=“identity”,fill=colour_hex_strings_all,width=1,position=
    position_dodge(width = 0.005))+scale_x_discrete(limits=
    sorted$colorname)+
    theme(axis.text.x  = element_text(angle=90, hjust=1,
    vjust=0.5,size=1))                                                                                                                                                                                             