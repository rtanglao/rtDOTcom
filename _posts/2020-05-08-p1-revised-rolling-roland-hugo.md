---
layout: post
title: "Revised workflow for rollingroland.com" 
---

# Pontifications

* You need to use "hugo" without `server` to render the site correctly for production i.e. non localhost

  ``` bash
  hugo server --buildDrafts --disableFastRender  --renderToDisk &
  hugo new post/2020-05-08-p1-vancouver-crossings.md
  # check it out at localhost:1313
  # When you are happy render and push to server
  hugo --buildDrafts #render
  surge public --domain rollingroland.com #push to server
  ```

  