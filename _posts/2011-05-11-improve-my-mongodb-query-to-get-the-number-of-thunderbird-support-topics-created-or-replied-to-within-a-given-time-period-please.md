---
layout: post
title: Improve my MongoDB query to get the number of Thunderbird support topics created
  or replied to within a given time period please
created: 1305149220
---
<p>I have a mongodb&nbsp; database created by my <a href="https://github.com/rtanglao/momogs/blob/master/mongoUpdateSlurpGS.rb">mongoUpdateSlurpGS.rb Ruby script</a> with Thunderbird Get Satisfaction support topics from July 20, 2009 until the present (i.e. roughly 40000 topics) and I would like to know for a given time period how many support topics were created or modified. To calculate this, I wrote a second ruby script called <a href="https://github.com/rtanglao/momogs/blob/master/alltopicsCreatedOrUpdated.rb">alltopicsCreatedOrUpdated.rb</a> (and the code is embedded below). My question is: is there really a need for a ruby script here.? Could the nested for "each" loop in <a href="https://github.com/rtanglao/momogs/blob/master/alltopicsCreatedOrUpdated.rb" target="_blank">alltopicsCreatedOrUpdated.rb</a>&nbsp; be replaced by a couple of mongodb queries using the <a href="http://www.mongodb.org/display/DOCS/dbshell+Reference#dbshellReference-CommandLine">mongodb command line interface</a>?</p><script type="text/javascript" src="https://gist.github.com/967386.js?file=mongoUpdateSlurpGS.rb"></script>
