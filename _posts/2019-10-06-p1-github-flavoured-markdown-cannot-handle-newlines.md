---

layout: post
title: 'Github flavoured markdown and most markdown implementations cannot handle newlines in tables: ruby solution: tr("\n", "")'
---

# Pontifications

* Yesterday I learned Github flavour markdown and most markdown implementations cannot handle newlines: ruby solution: trim("\n", "'')
* See [https://github.github.com/gfm/#tables-extension-](https://github.github.com/gfm/#tables-extension-) : "Block-level elements cannot
  be inserted in a table."
* [Solution](https://github.com/rtanglao/rt-kits-api2/blob/master/print-desktop-en-us-osx-increasing-ids-time-url-title-content.rb):

```ruby
tr("\n","")
```

