---
layout: post
title: MongoDB is my current persistent data structure store of choice aka "how to
  slurp your Get Satisfaction data into MongoDB"
created: 1301900488
---
<p>Got some data that you want to persist and manipulate but you are not sure what to do with it i.e. you are in exploratory or "side project" mode? Then <a href="http://www.mongodb.org/">MongoDB</a> is a fine choice in 2011. Easy to get the data in and out and then when you have figured out what you want to do when you grow up :-) you can store it in a "real" database as well e.g. PostgreSQL. e.g. If you want to get your data out of Get Satisfaction or any other system with an API for backup and other purposes, check out my "hacked in an hour or two but I think it works", <a href="https://github.com/rtanglao/momogs/blob/master/mongoUpdateSlurpGS.rb">mongoUpdateSlurpGS ruby script</a>. I used it to slurp in 20000 Get Satisfaction Thunderbird Topics and their associated replies and tags. If you want to do the same for your Get Satisfaction community, it's trivial to do: all you need is about 1 hour of a ruby (or other language,the code is pretty elementary) developer's time and some time to run the script.</p>
