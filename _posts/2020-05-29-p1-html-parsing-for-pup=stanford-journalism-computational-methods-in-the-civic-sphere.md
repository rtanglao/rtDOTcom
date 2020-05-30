---
layout: post
title: "HTML parsing for pup - Using the pup tool to more sanely extract data from HTML files (Stanford Journalism Computational Methods in the Civic Sphere)" 
---

# Pontifications

* **QUOTE**-->While [grep](http://www.compciv.org/recipes/grep/basic-of-grep) and [regular expressions](http://www.compciv.org/recipes/grep/basic-regex) are a powerful way to search raw text, when text files already have *structure* – such as comma-delimited files, or raw HTML – we want to take  advantage of programs specifically designed to exploit that structure.  With HTML, especially, finding a pattern *regular* enough (nevermind simple) that a regex can exploit is madness.

  So this is [why we're using pup](https://github.com/ericchiang/pup), which works from the command-line. Every other parsing library ([such as Python and BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/bs4/doc/)) you use will pretty much act the same as pup.

  I recommend just trying out pup, as described in the rest of this guide. The *arguments* it takes are [CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/Selectors), which you may be familiar with if you've ever used [JQuery](http://api.jquery.com/category/selectors/).

  However, you don't have to *know* CSS (i.e. how to style webpages) to do HTML parsing. You just have to understand how **CSS Selectors** are used to *target* specific HTML elements. Instead of *styling* these HTML elements, we will be grabbing the *text* inside them. Different purpose, but same process and syntax of *selection*. <-- **END QUOTE** ---> Read the whole thing [HTML parsing for pup - Using the pup tool to more sanely extract data from HTML files](http://www.compciv.org/recipes/cli/pup-for-parsing-html/) (Stanford Journalism Computational Methods in the Civic Sphere) <--- fantastic HOWTO

* Previously: [pup for HTML is like jq for JSON](http://rolandtanglao.com/2020/02/16/p2-pup-for-html-like-jq-for-json/), [How To get all Firefox Desktop SUMO KB Articles using pup WITHOUT using grep by using 'attr{href}'](http://rolandtanglao.com/2020/05/14/p2-how-to-get-all-firefox-desktop-urls-using-pup-without-grep/)

