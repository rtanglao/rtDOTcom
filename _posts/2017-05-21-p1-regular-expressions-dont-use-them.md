---
layout: post
title: When to use regexes aka regular expressions
---

## Pontifications

* Use an HTML parser instead of regular expressions
* Use a parser if you need a parser. Regular expression are not for your Domain Specific Language :-) !
* Use your language's built-in string search functions.
* As a last resort, [if you must use regexes, turn off white space significance and comment your regular expressions](https://blog.codinghorror.com/regular-expressions-now-you-have-two-problems/) (and test them on an online regular expression checker or some tool like [RegexBuddy](http://www.regexbuddy.com/)).