---
layout: post
title: If you want integers don't use strftime 
---
## Pontifications

* If you want integer values don't use something that returns strings :-) and then cast (or rely on casting) them to integers.
* In particular don't use ```strftime``` to get the integer day of the year like I did originally in [addDayOfTheyYear.rb](https://github.com/rtanglao/rt-ff48-rust/commit/7d5d03d03f8effed95606c53c1c986b2352d6585) instead use the integer API e.g. in [addDayOfTheyYear.rb](https://github.com/rtanglao/rt-ff48-rust/blob/master/addDayOfTheyYear.rb) :

```ruby
t = Time.at(row[1].to_i)
s = t.yday #not strftime !!!!!
year = t.year #not strftime !!!!!!!!!
```