---
layout: post
title: "Not sure why R's if_else() fails! Type system misunderstanding? Misunderstanding of NA?"
---
* The following is me trying to convert my 2019 and 2020 flickr photos' average colour to one of 657 R standard colours instead of the possible 256xx256x256 = 16777216  colours.
* It's probably my misunderstanding and a type issue R but not sure why the following never executes the `if` portion and always executes the `else` portion (full code is in [my repo over on github]()):
```R
if_else(synth_75imaveragecolour == "<NA>", as.hexmode(0), getnumericColour(synth_plotrixcolour)))
```
* I also tried `is.na()` and `== ""` and neither of those worked
* It's probably my misunderstanding of the R type system!
* I think I can diagnose this further by writing a loop (!) and printing out the values and the types

