---
layout: post
title: "Moving blogging to old MacBook Air in preparation for move to new Windows Machine"
---

## Pontifications

* First I had to install ruby:

```bash
brew upgrade rbenv ruby-build
rbenv global 2.5.0
vi ~/.bash_profile # and add eval "$(rbenv init -)"
```

* Then jekyll and surge.sh

```bash
gem install jekyll # my syntax colouring needs red carpet
gem install redcarpet
sudo npm install --global surge
```