---
layout:post
title: "Re-installing latest ruby, mongodb, node, surge, jekyll on WSL"
---
# 17december2018 install mongodb 4.0.4

* https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#install-the-mongodb-packages

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

# 17december2018 install node and surge

```bash
curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install --global surge
```
# 17december2018 add exclusion for Windows Defender

* https://medium.com/@leandrw/speeding-up-wsl-i-o-up-than-5x-fast-saving-a-lot-of-battery-life-cpu-usage-c3537dd03c74


# 17december2018 after re-install of Windows 10, install ruby 2.5.3

```bash
sudo apt-get update
sudo apt-get install build-essential
cd
wget http://ftp.ruby-lang.org/pub/ruby/2.5/ruby-2.5.3.tar.gz
tar -xzvf ruby-2.5.3.tar.gz
cd ruby-2.5.3/
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
