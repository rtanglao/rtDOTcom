---
layout: post
title: Public Suffix ruby gem by Simone Carletti gets me the Domain Name
---

## Pontifications
The [Public Suffix](https://github.com/weppos/publicsuffix-ruby) ruby gem by a Simone Carletti  gets me the domain name! yay! Thanks! [Public Suffix blog post](https://simonecarletti.com/blog/2010/06/public-suffix-list-library-for-ruby/)! 

### Code

[Here's how I used it to get domain names from URLs for Mozilla Lithium CSP](https://github.com/rtanglao/rt-csp/blob/master/README.md#22march2017).
From [print-domain.rb](https://github.com/rtanglao/rt-csp/blob/master/print-domain.rb):

```ruby
#!/usr/bin/env ruby
require 'rubygems'
require 'ccsv'
require 'uri'
require 'public_suffix'

header = true
Ccsv.foreach(ARGV[0]) do |values|
  $stderr.puts(values)
  if header == true
    header = false
    next
  end
  field2 = values[2]
  $stderr.printf("2nd record:%s\n",field2) # values[2] to get the URI
  if field2.index("https://") != 0 && field2.index("http://") != 0
    $stderr.printf("SKIPPING non HTTP and non HTTP FIELD2:%s; FIELD3:%s\n", field2, values[3])
    next
  end
  uri = URI.parse(values[2])
  begin
    domain = PublicSuffix.parse(uri.host)
    puts domain.domain
  rescue PublicSuffix::DomainNotAllowed
    $stderr.printf("PublicSuffix::DomainNotAllowed^^^ URI:%s\n", uri.host)
  end
end

```