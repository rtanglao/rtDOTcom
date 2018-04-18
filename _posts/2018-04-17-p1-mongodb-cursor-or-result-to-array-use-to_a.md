---
layout: post
title: "How to convert MongoDB cursor or result iterator to an array in Ruby: use 'to_a()'"
---

## Pontifications

* Example in ruby: 

```ruby
 result_array = reviewsColl.find(
   { 'id' => r1["id"] }).update_one(
     r1, :upsert => true ).to_a
```



