---
layout: post
title: "Installing Ruby 2.4.2 on GPD Pocket Running Ubuntu 16.04"
---

## Pontifications

* I followed the instructions on the GPD pocket at [Setup Ruby On Rails on
Ubuntu 16.04 Xenial Xerus](https://gorails.com/setup/ubuntu/16.04)

Specifically

```bash
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev\
 build-essential libssl-dev libreadline-dev\
  libyaml-dev libsqlite3-dev sqlite3\
   libxml2-dev libxslt1-dev libcurl4-openssl-dev\
    python-software-properties libffi-dev nodejs
    
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL

rbenv install 2.4.2
rbenv global 2.4.2
ruby -v

gem install bundler
```