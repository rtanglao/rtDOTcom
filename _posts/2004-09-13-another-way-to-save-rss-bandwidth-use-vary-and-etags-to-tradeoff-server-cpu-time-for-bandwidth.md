---
layout: post
title: " Another way to save RSS bandwidth - use Vary and ETags to tradeoff server
  CPU time for bandwidth"
created: 1095107487
---
<p>
Interesting.  I don't know if this is the be all and end all of solutions but it's definitely a start! My gut says that there is a simpler solution.
</p><p>
From <a href="http://www.intertwingly.net/blog/2004/09/11/Vary-ETag">Sam Ruby: Vary: ETag</a>:
</p><p>
<strong>QUOTE</strong>
</p><blockquote>
Another bandwidth reduction idea, compliments of FooCamp04.
<br />
<br />This idea doesn't require coordination between vendors, and leverages the ETag support that is present in many existing aggregator clients.  It is complicated to explain, and would be complicated to implement, but the end result would take the form of an Apache Module (and/or IIS filter) that sysadmins of major sites could just "drop in".
</blockquote><p>
<span style="font-size:12pt;">
<br /></span><strong>UNQUOTE</strong><span style="font-size:12pt;">
<br /></span>
</p>

