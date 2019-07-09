---
layout: post
title: Pry instead of ruby irb?
---

## Pontifications

* Anybody use [pry](http://pryrepl.org/) instead of the ruby irb repl?
* [Jason Arnold's Pry tutorial from 2016 makes it look simple](https://medium.com/@thejasonfile/one-step-forward-while-prying-into-ruby-code-1020c2ee12bc) (and [richonrails has a nice tutorial](https://richonrails.com/articles/easier-debugging-with-pry)), just add:

```
1. Install the pry gem. 
2. Add the “require ‘pry’” line to the top of your Ruby file. 
3. Add the ‘binding.pry’ line to the location in your script where you want it to stop and open it in Pry.
4. Control D to continue
5. !!! to exit Pry early
```