---
layout: post
title: How to narrate your work using a github repo, emacs and README.md
---

tl;dr: narrate your work using README.md, a github repo, and emacs aka ```control-X VV``` is your friend

## Pontifications

(the following assumes you have a Linux or Mac computer and have installed git and emacs (I use [Aquamacs](http://aquamacs.org/)); if you have Windows I'm sorry :-) perhaps someday the Windows Unix subsystem will work; in fact that day won't be long from now)

git and github repos aren't just for software development, you can use them for blogging :-) ! and narrating your work!

Narrate ([can't believe I used document instead of narrate in my blog post](http://rolandtanglao.com/2016/11/11/p1-document-your-work-and-your-facts-using-html-and-markdown/)) **as you work, not after**! Because you will forget if you do it after!

* 1\. [create a github repo with a README.md](https://github.com/new)  (make sure you have checked ``` Initialize this repository with a README```)
* 2\. [clone it on your computer](https://help.github.com/articles/cloning-a-repository/)
* 3\. edit README.md; my conventions ([sample README.md with examples of the following conventions](https://github.com/rtanglao/rt-animated-gifs)) are:
    * second level heading i.e. ```##``` for the date e.g. November 15, 2016 - Then you have a permalink for the date.
    * bullet list for your what you did whether it's code or writing or whatever using ```*```.
    * if it gets complicated create subsections using h3 i.e. ```###```
    * if your README.md gets complicated, then use emacs to fold i.e. hide the other days (position your curser at the column 0  of the line you want to hide and then ```Markdown Menu -> Show/Hide -> Cycle visibility``` to toggle hiding and showing the lines below the cursor)
* 4\. commit your changes (using emacs it's as simple as ```control-XVV```, type your commit reason and then ```control-CCC``` and then git pull ; easy :-) !)
* 5\. ```git push```

## Wow that's hopelessly complicated and geeky?!?

Yes it is :-) but once you figure it out it is quite powerful and your README.md becomes your blog (with the url of your github repo being the homepage) and you can make changes quickly.

Yes I know you can make a github.io sites but that is even more complicated :-) !