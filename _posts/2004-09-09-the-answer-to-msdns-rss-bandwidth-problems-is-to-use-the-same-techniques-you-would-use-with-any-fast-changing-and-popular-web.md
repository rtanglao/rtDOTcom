---
layout: post
title: " The answer to MSDN's RSS bandwidth problems is to use the same techniques
  you would use with any fast changing and popular web"
created: 1094799163
---
<p>
What PhotoMatt said. Use the Force, er HTTP, Luke!
</p><p>
From <a href="http://photomatt.net/2004/09/09/rss-bandwidth-usage/">Photo Matt - RSS Bandwidth Usage</a>:
</p><p>
<strong>QUOTE</strong>
<br />
</p><blockquote>
My front page is an average of 17K HTML and about 30K of images, so lets say 50K. The images and CSS are all cached, but I don&#8217;t output the proper headers on the HTML because it would be a pain. I would have to check the time of the latest post, check the latest updated link, make sure there&#8217;s not a random photo, basically go through a lot of trouble that isn&#8217;t really worth it. (When I was caching everything with Staticize the page was stored in its entirety so I sent correct headers, but I don&#8217;t bother with that anymore because everything is so fast it doesn&#8217;t really make a difference.) All that said, I&#8217;m happy with the level of optimization, my HTML and CSS is as streamlined as I want it to be.
<br />
<br />My feed, on the other hand, is completely self-contained. I can send headers with confidence because I know everything in that file and can say authoritively when it was last changed. (Actually WordPress handles it all automatically, I don&#8217;t worry about it.) Most of the aggregators that hit my site support this. I don&#8217;t think about it and they don&#8217;t think about it, HTTP just works. My feed has 25 items because of my posting frequency, more than twice the number of items most feeds have. The feed is usually around 10K, and as I already mentioned it&#8217;s only one request.
<br />
<br />Here&#8217;s the kicker: my RSS feed is requested 3 times for every time my front page is loaded. So a HTML page with 1/3 the traffic is using over 30 times the bandwidth. What was that about scalability again?
</blockquote><p>
<strong>UNQUOTE</strong>
</p>

