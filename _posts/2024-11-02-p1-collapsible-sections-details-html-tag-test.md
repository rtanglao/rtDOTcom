---
layout: post
title: 'Collapsible Sections work but you need an markdown="1" attribute in the details tag and markdown="span" in the summary tag'
---
##  Collapsible markdown works

* You need a `markdown="1"` attribute in the `details` tag and `markdown="span"`` `in the `summary` tag
* Hat tip to the folks who found this in github.com issue: [Update docs for "Organizing information with collapsed sections" to include GitHub Pages support #32988](https://github.com/github/docs/issues/32988) 

<details markdown="1">
<summary markdown="span">Click me</summary>
### yes, even collapsed code blocks work 
```python
print("hello world!")
```
</details>

### Full code from issue 32988

```
<details markdown="1">

<summary markdown="span">Tips for collapsed sections</summary>

### You can add a header

You can add text within a collapsed section. 

You can add an image or a code block, too.

```ruby
   puts "Hello World"
\`\`\` <-- unescape the backslashes for your actual blog post!

</details>

```


## Previously

*  November 26, 2018: [HTML tags  and  can be used for expand/collapse with disclosure triangles for 'collapsible HTML'](http://rolandtanglao.com/2018/11/26/p1-collapsing-and-expanding-disclosure-triangles-using-details-summary-html-tags/)        
