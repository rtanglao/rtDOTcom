---
layout: post
title: Alpha Equivalence in Lambda Calculus from the Haskell book by Allen And Moronuki
---

From page 45 of [Haskell Programming from first Principles by Christopher Allen and Julie Moronuki](http://rolandtanglao.com/2016/09/09/p1-learning-me-a-haskell/):

## Update 11 September 2016 screenshot of desktop for mobile users!

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/29520118621/in/dateposted-ff/" title="alpha equivalence in lambda calculus 20160911_005625"><img src="https://c6.staticflickr.com/9/8485/29520118621_cfd34ea977.jpg" width="500" height="500" alt="alpha equivalence in lambda calculus 20160911_005625"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

## Exercise

```
3. 𝜆𝑥𝑦𝑧.𝑧𝑥
a) 𝜆𝑥.(𝜆𝑦.(𝜆𝑧.𝑧)) 
b) 𝜆𝑡𝑜𝑠.𝑠𝑡
c) 𝜆𝑚𝑛𝑝.𝑚𝑛
```
Which is correct? 

I believe the answer is b). 

Not a) because a) omits ```x```. 

Not c) because c) should be ```𝜆𝑚𝑛𝑝.𝑝𝑚``` NOT```𝜆𝑚𝑛𝑝.𝑚𝑛```


