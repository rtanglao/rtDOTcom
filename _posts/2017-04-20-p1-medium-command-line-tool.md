---
layout: post
title: Link Blog medium command line tool -- url, title, link text
---

## Pontifications

* [See yesterday's initial discussion of my to-be-written medium command line link-blogging-to-rolandtanglao.com tool](http://rolandtanglao.com/2017/04/19/p1-medium-still-not-my-fav-but-i-will-make-it-my-link-blog/)
* Current thinking: 
    * url is mandatory parameter - the url of the blog post on rolandtanglao.com
    * optional is title  - (if not specified use title of the blog post)
    * linktext is mandatory and specifies the text that links to the blog post 
* Sample invocation:

```bash
./link-blog.rb \
-url \
http://rolandtanglao.com/2017/04/19/p1-medium-still-not-my-fav-but-i-will-make-it-my-link-blog/ \
-title "Medium could be a cool link blog" \
-linktext \
"Still not a fan of Medium but I'll grudgingly admit it gets good flow"
```
