---
layout: post
title: tc a function to get the top colour name in R
---

    tc <-
    function(x) {
    return (head(color.id(x),n=1))
    }