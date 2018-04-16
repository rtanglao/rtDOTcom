---
layout: post
title: "How to turn off MongoDB logging in the ruby driver"
---

## Pontifications

* I thought I blogged this previously :-) ! I guess I didn't!

```ruby
Mongo::Logger.logger.level = Logger::FATAL
```



