---
layout: post
title: "How to install ruby 2.5.1, jekyll and surge on surface book 2, Windows 10 WSL as of June 1, 2018"
---

## Pontifications

* works for me no warranty etc :-) from: [https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me/blob/master/README.md#01june2018](https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me/blob/master/README.md#01june2018) 

```bash
sudo apt-get update
sudo apt-get install build-essential
cd
wget http://ftp.ruby-lang.org/pub/ruby/2.5/ruby-2.5.1.tar.gz
tar -xzvf ruby-2.5.1.tar.gz
cd ruby-2.5.1/
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
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs 
sudo npm install --global surge
sudo add-apt-repository ppa:git-core/ppa
sudo apt update; sudo apt install git
```



