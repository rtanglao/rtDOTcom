---
layout: post
title: " We need a better way to track and continue conversations"
created: 1082872872
---
This shows the crudeness of today's blogging tools.  To the non-developer, it's absurd  we don't have something as simple sounding as "reply on my blog". Unfortunately as always, the simplest sounding things are the hardest to implement and Jamie Pitts is one of the few developers who has thought it through.

From <a href="http://www.semanticwave.com/blog/archives/000120.jsp">Semantic Wave: TalkBack: Reply on My Blog</a>:
<p><strong>QUOTE</strong></p><blockquote>Blog-to-blog conversations are easily fragmented, with responses residing on blog discussion boards, the responder's site, and on various tracking services.

I have been thinkin about how to implement a "reply on my blog" link which would enable a writer to reply using his own CMS.

Implemented with current web technology, this idea assumes that the API of the responder's blogging software can be known to the site which he is responding to. This reply would link to a script on the original site, which, after noting the action, would redirect the request to the content management system under the responder's control.

RDF for the original entry (and historical data about the conversation) would be passed to the responder's CMS in the url string. He would respond. As his CMS updates his blog, his response would be forwarded on to the cited blog (which would be expecting it), trackers, aggregators, and online communities.</blockquote><p><strong>UNQUOTE</strong></p>

