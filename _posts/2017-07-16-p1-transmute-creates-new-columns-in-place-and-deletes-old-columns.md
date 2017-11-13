---
layout: post
title: R transmute() creates new columns and deletes old columns unlike mutate() which add the columns at the end
---

## Pontifications

* Following up on [Reverse Engineering R joyplot code part 4 - Need to figure out what "%>%" really means and what tidyverse and transmute() do](http://rolandtanglao.com/2017/07/14/p1-joyplot-example-reverse-engineering-part4-need-to-figure-out-tidyverse-lubridate-transmute/), here's what ```transmute()``` does!
* From [R for Data Science - 5.5  Add new variables with mutate()](http://r4ds.had.co.nz/transform.html#add-new-variables-with-mutate):

**QUOTE**

<blockquote>

"Besides selecting sets of existing columns, it’s often useful to add new columns that are functions of existing columns. That’s the job of mutate()<br /><br />
...<br /><br />
If you only want to keep the new variables, use transmute()"

</blockquote>

**END QUOTE**

