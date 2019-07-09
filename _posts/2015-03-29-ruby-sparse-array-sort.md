---
layout: post
title: How to create a sparse array in Ruby and sort by value
---
Saving for later:

    a = Hash.new(0)
    a[4]=2
    a[1]=3
    a[555] = 20
    a.sort_by {|k,v| v}.reverse
    => [[555, 20], [1, 3], [4, 2]]