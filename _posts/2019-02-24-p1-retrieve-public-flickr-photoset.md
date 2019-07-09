---
layout: post
title: "get-set-photo-metadata.rb - Ruby code to download metadata from a  flickr set of photos i.e an album"
---

# Pontifications

* To use [get-set-photo-metadata.rb](https://github.com/rtanglao/for-jmv-pm-photos/blob/master/get-set-photo-metadata.rb), first setup mongoddb

```bash
cd /home/roland/GIT/for-jmv-pm-photos
. ./setupFlickrjmvpmDB
```

* and then specify two parameters: the flickr alphanumeric userid and the flickr set id

```bash
./get-set-photo-metadata.rb 36896321@N08 72157622068072145
```