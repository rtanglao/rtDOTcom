---
layout: post
title: " Lifeblog is yet another app that gratuitously uses the Atom API"
created: 1103672544
---
<p>&lt;rant&gt;After skimming the PDF, I see no reason why Lifeblog didn't use the MetaWeblog API over SSL rather than the Atom API.  After all, everything on a phone is either text, SMS (which is text), photos, audio or video all of which can be handled by the Meta Weblog API's newMediaObject call.  And passages like this would worry me if I was implementing this: "Since the Atom API (as it stands in version 0.9 draft) does not support posting of non-post resources (such as non-post images) and certain item types (such as SMS), the Lifeblog posting uses some non-standard features. Care has been taken to ensure compatibility with &ldquo;pure&rdquo; Atom (draft) server implementations (as long as the server doesn&rsquo;t mind extra non-Atom elements in the &lt;entry&gt; element), so Lifeblog should still work with those (although with missing functionality)."&lt;/rant&gt;</p> <p>From <a href="http://cognections.typepad.com/lifeblog/2004/12/lifeblog_postin.html">Lifeblog: Lifeblog posting protocol specification 1.0</a>.:</p>
<p><b>QUOTE</b></p><blockquote><p>This is the technical document that explains how we use Atom to post multimedia content online. Use this document to figure out how to adapt your servers to use Lifeblog 1.5.</p>

<blockquote><p><a href="http://cognections.typepad.com/lifeblog/files/lifeblog_posting_protocol_specification_1.0.pdf">Download the Lifeblog posting protocol specification 1.0.pdf
</a></p></blockquote>
</blockquote><p><b>UNQUOTE</b></p>



