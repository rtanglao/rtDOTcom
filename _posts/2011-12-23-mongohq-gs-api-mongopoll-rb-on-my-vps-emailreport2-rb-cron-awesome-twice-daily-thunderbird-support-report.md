---
layout: post
title: mongohq + GS API + mongoPoll.rb on my VPS + emailReport2.rb + cron = awesome
  twice daily Thunderbird support report
created: 1324685708
---
<p>mongohq&nbsp; + <a href="http://getsatisfaction.com/developers/api-resources">GS API</a> +&nbsp; <a href="https://github.com/rtanglao/momogs/blob/master/mongoPoll.rb">mongoPoll.rb</a> on my VPS +<a href="https://github.com/rtanglao/momogs/blob/master/emailReport2.rb"> emailReport2.rb</a> + cron = awesome twice daily Thunderbird support report with trending tags, topics, anti-virus, ISPs and mail providers on <a href="http://thunderbirdrobot.posterous.com/">posterous </a>and in my inbox. Code is open source. Pull requests welcome!</p><h3>Bugs</h3><ol><li><a href="http://developers.posterous.com/html-limits-on-posts-via-email-or-the-api">posting to posterous via email or the API results in truncated posts</a> (I guess that's what happens when you have 2500 line long posts :-)! )</li></ol><h3>features that i intend to add:</h3><ol><li>trending Thunderbird add-ons</li><li>trending nouns that aren't: ISPs, Mail Providers, anti-virus, tags or add-ons</li><li>remove polling, use Web Hooks instead</li></ol>
