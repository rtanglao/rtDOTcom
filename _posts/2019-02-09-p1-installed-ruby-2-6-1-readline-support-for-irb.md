---
layout: post
title: "Installed ruby 2.6.1 on WSL with readline support so irb cursor keys work, here's how"
---
# Pontifications

* Basically the same as [ruby 2.5.3](https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me/blob/master/README.md#17december2018-after-re-install-of-windows-10-install-ruby-253) but I changed ```2.5.3``` to ```2.6.1``` and installed ```libreadline-dev```

```bash
sudo apt-get update
sudo apt install -y libreadline-dev
sudo apt-get install build-essential
cd
wget http://ftp.ruby-lang.org/pub/ruby/2.6/ruby-2.6.1.tar.gz
tar -xzvf ruby-2.6.1.tar.gz
cd ruby-2.6.1/
sudo apt-get install zlib1g-dev
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt-get install libssl-dev
./configure
make
sudo make install
ruby -v
sudo gem update --system
sudo gem install jekyll bundler
sudo gem install redcarpet
```