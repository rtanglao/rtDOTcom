---
layout: post
title: "Installed ruby 2.5.0 on Windows 10, couldn't get rvm or rbenv to work"
---

## Pontifications
 

From [Setup Ruby On Rails on Ubuntu 16.04 Xenial Xerus](https://gorails.com/setup/ubuntu/16.04), here's how I installed ruby 2.5.0 on Windows 10 (I couldn't get rbenv to work and the CSV gem wouldn't work on [ruby 2.3 which is what I installed before](http://rolandtanglao.com/2018/02/27/p1-jekyll-surge-windows/) )

```bash
cd
wget http://ftp.ruby-lang.org/pub/ruby/2.5/ruby-2.5.0.tar.gz
tar -xzvf ruby-2.5.0.tar.gz
cd ruby-2.5.0/
./configure
make
sudo make install
ruby -v
```