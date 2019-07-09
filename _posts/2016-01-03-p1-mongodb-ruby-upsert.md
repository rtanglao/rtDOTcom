---
layout: post
title: upsert using ruby 2.3, mongodb 3 and driver 2
---

[Update and insert all in one go](https://github.com/rtanglao/rtgram/commit/92a58561d583563559ef0cd9018c552dce590b53#diff-7bb9d9fb060d2d3ad8f4588659887d3d)! (I’m sure this worked with ruby mongo driver version 1. I just didn’t realize it until I read [this stackoverflow question on upsert](http://stackoverflow.com/questions/30772689/i-could-not-push-an-new-data-into-array-when-use-upsert)). Here’s the relevant code snippet (“id” is the instagram string unique id not to be confused with mongo’s unique id which is “_id”):

``` ruby
photosColl.find({ 'id' => id }).update_one(photo,:upsert => true )    
```                                                                                                                                                                                       