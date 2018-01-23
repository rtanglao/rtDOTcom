---
layout: post
title: "Ruby tip: no need to iterate over an array to print it, ruby does the right thing, just call puts"
---

## Pontifications

* Simple ruby tip today [following up from yesterday](http://rolandtanglao.com/2018/01/21/p1-2018-querying-mongodb-by-date-and-integer-value/):
* No need for:

```ruby
q["content"].split(' ').each {|c| puts c}
```

* because ```puts``` does the right thing, all you need to do is:

```ruby
puts q["content"].split(' ')
```