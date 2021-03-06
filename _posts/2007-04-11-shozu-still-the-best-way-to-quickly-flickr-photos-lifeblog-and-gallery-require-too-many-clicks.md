---
layout: post
title: ShoZu still the best way to quickly flickr photos, Lifeblog &  Gallery require
  too many clicks
created: 1176287028
---
<p>
For me, ShoZu is still the best way to flickr photos. I can't imagine not using it in spite of the bugs that Ken, Alec and others have observed. When it works, it is fast and easy and requires 0 clicks (or 2 if you don't automagically upload the photos as they are taken).
</p><p>
I have tried LifeBlog (hate the Windows and PC centric world view (it's about the cloud not the PC!) and the fact that you can only upload 6 photos at a time and the many clicks and how it's quite easy to upload the same photo twice since there's no UI cues for which photos have been uploaded) and the Gallery App on the N93 (again only 6 photos at at time and way too many clicks!)
</p><p>
ShoZu worked much better for me on the Nokia N70 (<a href="http://flickr.com/search/?w=35034347371%40N01&amp;q=shozu+n70&amp;m=tags">2237 photos uploaded to flickr via ShoZu</a>) and 7610 (<a href="http://flickr.com/search/?w=35034347371%40N01&amp;q=shozu+7610&amp;m=tags">814</a> photos dating back to October 2005)  i.e. S60v2 I think! I have had the same issues as <a href="http://ipadventures.com/?p=1711">Ken</a> and <a href="http://saunderslog.com/2007/04/10/shozu-not-ready-for-prime-time/">Alec</a> on all my S60v3 phones i.e. N80i (<a href="http://flickr.com/search/?w=35034347371%40N01&amp;q=shozu+n80i&amp;m=tags">701 photos</a>; which unfortunately seems to have memory issues in general even with the latest firmware), N73 (<a href="http://flickr.com/search/?w=35034347371%40N01&amp;q=shozu+n73&amp;m=tags">178 photos</a>) and N93 (<a href="http://flickr.com/search/?w=35034347371%40N01&amp;q=shozu+n93&amp;m=tags">152</a>). The N93 with the latest firmware runs ShoZu better I think.
</p><p>
As a former software developer who currently tests software (Drupal), who as well writes software documentation for Drupal, it annoys me that I can't seem to definitively pin down the reason for the instability of ShoZu on S60v3 nor can I reproduce it a will.
</p><p>
Some guesses (I would call them theories but I am unencumbered by S60 developer knowledge!):
</p><ol>
<li>Symbian memory allocation/deallocation/leaks</li>
<li>S60 memory allocation/deallocation/leaks</li>
<li>ShoZu memory allocation/deallocation/leaks</li>
<li>Clash with the phone's thumbnail creation code (I have noticed that if you go into the gallery, the thumbnails can take many many seconds to appear and when they don't appear ShoZu doesn't work. Coincidence? Maybe!)</li>
<li>The auto upload code hogs the CPU?!?</li>
</ol><p>
I am trying to test #5 by turning off auto upload. Currently have 98 photos on my N93. We'll see if the instability starts up again after 120 or so photos as seems to be the pattern. Any help or clues would be appreciated
</p><p>
FROM <a href="http://saunderslog.com/2007/04/10/shozu-not-ready-for-prime-time/">ShoZu. Not ready for prime-time. -- Alec Saunders .LOG</a>:
</p><p>
<strong>QUOTE</strong>
</p><blockquote>
Ken Camp has a love / hate relationship with Shozu.  I have to say that I concur.  It's unbelievably promising, and purports to solve a problem that I have — that Nokia's LifeBlog software doesn't target Wordpress.  However, it took hours last night to remove it from the phone.  Once installed, it takes over the phone entirely. Hopefully they can solve the problems quickly.
</blockquote><p>
<strong>END QUOTE</strong>
</p>
