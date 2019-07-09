---
layout: post
title: Ruby '..' aka "2 dot" range operator is inclusive, '...' aka "3 dot" range operator is exclusive
---

## Pontifications

* [Ranges constructed using .. run from the beginning to the end inclusively. Those created using ... exclude the end value. ](http://ruby-doc.org/core-2.1.3/Range.html)
* It's not like C! ```variable[0,n]``` is the same as ruby's ```variable[0..n]```. In ruby ```variable[x,n]``` means starting at position x, return n elements. Learned this the hard way in [production-test-797-redirects.rb](https://github.com/rtanglao/rt-li-sumo-redirects/blob/master/production-test-797-redirects.rb)

```ruby
#using ranges. The end position is included with two periods but not with three
array_four[0..1]              # => ["a", "b"]
array_four[0...1]             # => ["a"]
```