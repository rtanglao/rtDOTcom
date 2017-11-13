---
layout: post
title: Use semi-colon to separate multiple statements in a block on a single line in ruby
---

## Pontifications
* 1\. only works with ```begin```...```end``` not ```{```...```}``` blocks

e.g. from multiple-statements-in-a-block.rb:

```ruby
#!/usr/bin/env ruby
require 'rubygems'

x = 1
begin puts "1" ; puts "2" end if x == 1
# note this doesn't work: { puts "1" ; puts "2" } if x == 1
# Why doesn't it work? probably because {} returns a value

```

output:

```bash
ruby multiple-statements-in-a-block.rb 
1
2
```

* 2\. explanation from [Interacting with Ruby Objects](https://www.sitepoint.com/learn-ruby-on-rails-2/):

<blockquote>

Chaining Statements Together<br /><br />

Ruby doesn’t require us to use any character to separate commands, unless we want to chain multiple statements together on a single line. In this case, a semicolon (;) is used as the separator. However, if you put every statement on its own line (as we’ve been doing until now), the semicolon is completely optional.<br /><br />

If you chain multiple statements together in the interactive shell, only the output of the last command that was executed will be displayed to the screen:
</blockquote>

* 3\. See also: [Mastering ruby blocks in less than 5 minutes](https://mixandgo.com/blog/mastering-ruby-blocks-in-less-than-5-minutes)