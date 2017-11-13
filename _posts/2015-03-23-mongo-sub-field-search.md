---
layout: post
title: MongoDB sub-field search queries
---
From
[reTryNoJpg.rb](https://github.com/rtanglao/rtgram/blob/gh-pages/reTryNonJpg.rb)
(to search for the url subfield using a url fragment):

    query = {"images.thumbnail.url" => /#{url_fragment}/i}
    photo = photosColl.find_one(query, :fields => ["images"])
