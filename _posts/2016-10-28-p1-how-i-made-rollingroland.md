---
layout: post
title: How I created RollingRoland.com using hugo, hover.com DNS and surge.sh
---
## UPDATE tl;dr

```sh
cd /Users/rtanglao/Dropbox/ROLLINGROLAND.COM_SURGE/rollingroland
hugo new post/2017-01-09-p1-snowmaggedon2016-7.md
# edit in IA Writer or other markdown editor:  content/post/2017-01-09-p1-snowmaggedon2016-7.md
hugo --theme=beautifulhugo --buildDrafts
surge public --domain rollingroland.com
```

## Pontifications

Since I'm sure I'll forget, here's how I created my new rollingroland.com blog using surge.sh and hugo and hover's DNS.

Step 0 is of course to buy the domain name. I recommend [hover](https://www.hover.com/)!

### hugo - the blog engine aka static site generator written in go

Install hugo using brew on Mac OS X or your favourite linux package manager.

* ```cd /Users/rtanglao/Dropbox/ROLLINGROLAND.COM_SURGE```
* Create fresh blog post: ```hugo new post/hello.md``` and edit in your favourite markdown editor e.g. IA writer
* ```cd themes ; git clone https://github.com/halogenica/Hugo/BeautifulHugo.git beautifulhugo ; cd ..```
* ```hugo server --buildDrafts --theme=beautifulhugo```
* Change draft in hello.md to "draft = false" when happy
* render the pages to the ```public``` subdirectory:  ```hugo --theme=beautifulhugo````

### hover.com - DNS changes

* create an A record: ```@ A 192.241.214.148```
* create a CNAME record: ```www CNAME	na-west1.surge.sh.```

### surge.sh - hosting the rendered pages

The following command posts the rendered pages to the [fabulous static hosting service surge.sh](http://surge.sh/):

* ```surge public --domain rollingroland.com```
