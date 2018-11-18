---
layout: post
title: "Cleaning the data to make it work with your data visualization toolkit is 90% of the work; to learn a new plotting technique take the sample code, print out the dataset  and and write your code to you create the identically structured dataset"
---

## Pontifications

* And it's not fun work but it is rewarding work because then you can easily plot using ```ggplot2``` or whatever you use!
* In fact it's not fun but data cleaning is also an act of judgement and analysis because it's almost always a judgment call as to what an 'outlier' is and what outliners to throw out!
* I'm far from the first to observe this of course :-)
* And ```ggplot2``` is great fun because you can easily create many many types of graphs with that 1 cleaned dataset with minimal lines of code.
* An example was the [previous post on the Operating System graph for Firefox Desktop questions](http://rolandtanglao.com/2018/11/15/p1-no-surprise-in-ff-desktop-questions/): e.g.  what is 'linux'? should I track every distro? You can see my arbitrary-but-hopefully-mostly-correct choices in [the ruby code to generate the dataset](https://github.com/rtanglao/rt-kitsune-api/blob/master/print-csv-os-percentage-group-label-title.rb):

```ruby
case os
  when /^Windows 7/i
    os = "Windows 7"
  when /^Windows 10/i
    os = "Windows 10"
  when /^Windows 8/i
    os = "Windows 8"
  when /^Windows XP/i
    os = "Windows XP"
  when /^Mac OS/i, /^macos/i
    os = "Mac OS"
  when /^Linux/i, /^ubuntu/i, /^centos/i, /^arch/i, /^lfs/i, /^fedora/i 
    os = "Linux"
  else 
    logger.debug "SETTING os:" + os + " to other"
    os = "Other"
end
```
