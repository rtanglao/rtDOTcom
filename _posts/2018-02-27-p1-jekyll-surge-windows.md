---
layout: post
title: "Getting jekyll, surge etc to work on Windows Linux Subsystem"
---

## Pontifications

* have to re-compile ruby from scratch otherwise jekyll gem won't build, no idea why :-)

```bash
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt-get install -y build-essential ruby-full
sudo gem update --system
sudo gem install jekyll bundler
sudo gem install github-pages
apt-get install zlib1g-dev
sudo apt-get install zlib1g-dev
sudo gem install github-pages # don't need this
sudo gem install redcarpet
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs 
sudo npm install --global surge
```