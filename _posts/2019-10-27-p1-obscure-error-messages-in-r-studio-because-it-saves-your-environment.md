---

layout: post
title: "R Studio: Reminder that you will get obscure error messages because R Studio saves and restores all your variables"
---

# Pontifications

* e.g. if you reference variable `x` and then rename it to  `y` but  forget to rename all instances of `x` to `y` then you won't get an undefined error for the remaining references to  `x`
* I guess you can avoid this by using R Studio's code editor renaming functions which I've never used.
