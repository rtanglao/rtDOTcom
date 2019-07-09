---
layout: post
title: "How to upsert a single mongodb field using the ruby 2 driver"
---

## Pontifications

where ```upsert``` means add it if not present, update if present

* From [add-answered-in-72-hours.rb](https://github.com/rtanglao/sumo-questions/blob/master/add-answered-in-72-hours.rb) an example of how to upsert a boolean, ```answered_in_72_hours```:

```ruby
questionsColl.find_one_and_update(
    { id: q["id"] }, { "$set" => { answered_in_72_hours: answered_in_72_hours }},
    :upsert => true)
```