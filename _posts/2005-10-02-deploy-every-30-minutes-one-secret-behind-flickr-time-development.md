---
layout: post
title: " Deploy every 30 minutes: One secret behind Flickr time development"
created: 1128267946
---
<p>Amen! In the future all web apps will use techniques like this! Go flickr go! Go <a href="http://www.rolandtanglao.com/archives/2005/03/22/yahoo_buys_flickr_flickrtime_rules_for_web_20_apps">flickrTime</a> development go!
</p><p>From <a href="http://blogs.warwick.ac.uk/chrismay/entry/deploy_every_30/">Deploy every 30 minutes: Redux, 25/08/05, Secret Plans and Clever Tricks</a>.:</p>
<p><b>QUOTE</b></p><blockquote><p>For most types of changes, the implementation is nothing more than a simple rsync from CVS HEAD onto the server farm. Sometimes an apachectl graceful, a squid/memcached flush or a restart of the various daemons is also required, but it's a zero-downtime thing even under peak loads.
</p>
<p>- A similar on-click rollback to any previous version if it all goes wrong.
</p>
<p>- A good separation of layers in the application to minimise liklihood of collateral damage from a change.</p>

<p>- A small team with pretty complete knowledge of the code that they're updating. (2 java programmers, 2 PHPers, a designer and a front-end guy)
</p>
<p>- A component-based application infrastructure with clear interfaces between components. Most application logic is coded in PHP, with cacheing provided via Squid and memcached, and key long-running daemon processes in java. Individual components can be redeployed with comparatively little risk to other components, so long as interfaces aren't modified.
</p>
<p>Surprisingly, there's not much weight put on automated testing. There are automated test suites for some key black-box components (the email parser for instance) and a few functional tess (written using perl's www:mechanize) but mostly they're reliant on developers testing on the staging server (though they now also have the services of yahoo's 'surfers' user-testing department).
</p>
<p>Well. Quite frankly I'm jealous. Not that I don't think we could do it too, but it would be a lot of work to get there from where we are now. ISTM, also, that the benefits of of this set-up are a bit like doing XP; until you actually get everything working together you don't see much benefit, but once you do, suddenly it changes all the rules.
</p></blockquote><p><b>UNQUOTE</b></p>



