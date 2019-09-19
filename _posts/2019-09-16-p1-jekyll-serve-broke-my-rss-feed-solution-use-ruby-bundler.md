---

layout: post
title: "Running jekyll serve broke my RSS feed; solution use ruby bundler in production mode"
---

# Pontifications

* ```jekyll serve``` broke my RSS feed (which [Ton discovered,](https://www.zylstra.org/blog/2019/09/9069/) thanks)
* The solution is to use the ruby bundler in production mode (after setting jekyll up with the ruby bundler as per the official docs: [Using Jekyll with Bundler](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/)):
  * namely ``` JEKYLL_ENV=production bundle exec jekyll serve```
