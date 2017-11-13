---
layout: post
title: Setting up a new Mac Book Pro on el capitan part 1
---
1. install xcode
https://itunes.apple.com/au/app/xcode/id497799835?mt=12
1. xcode-select --install
1. ruby -e "$(curl -fsSL
https://raw.githubusercontent.com/Homebrew/install/master/install)"
1. brew install rbenv ruby-build
1. Add rbenv to bash so that it loads every time you open a terminal
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile
1. rbenv install 2.2.3
1. rbenv global 2.2.3
1. ruby -v
1. gem install jekyll
1. brew install node
1. npm install --global surge
1. gem install redcarpet
1. gem install rouge
1. in _config.yml added highlighter: rouge comment out #pygments: true
