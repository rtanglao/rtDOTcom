---
layout: post
title: "Windows files are UTF-16 NOT UTF8, how to read them in ruby: 'rb:bom|utf-16'"
---

## Pontifications
 

From [read-reviews-replies.rb](https://github.com/rtanglao/rt-fennec-gplay/blob/master/read-reviews-replies.rb) :

```ruby
CSV.open(ARGV[0], 'rb:bom|utf-16', :headers => true) do |csv|
  csv.each { |row| ap row }
end
```

where: ```rb``` is read, binary (utf16 files are not text files!)