---
layout: post
title: How To -- Linux core utilities instead of OS X BSD style utilities specifically split and grep 
---

tl;dr: On OS X you might want linux style utilities instead of OS X's BSD style utilities

## Pontifications

I have been using Unix since 1985 and as a result I get all split, grep and all the utilities mixed up, so glad we can use all of the simultaneously :-) !

* To get [gnu core utilities](https://www.gnu.org/software/coreutils/coreutils.html) like [split](https://www.gnu.org/software/coreutils/manual/coreutils.html#split-invocation) (called gsplit by default on OS X to prevent breaking scripts that rely on BSD split): <br />```brew install coreutils```
* To get BSD style grep (again called ggrep to prevent breaking scripts that rely on BSD grep):<br />```brew install homebrew/dupes/grep```
* previous post on [gsplit](http://rolandtanglao.com/2016/11/04/p1-gsplit-to-split-files-into-chunks/)
