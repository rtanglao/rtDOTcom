---
layout: post
title: JS Static Site Generator in your browser that renders to S3 or cloud storage that offers web hosting = easy self hosted web site for the 21st century
---

**tl;dr** Browser based see + cloud storage + simple web hosting for that cloud storage = 21st websites for everyone!

## Pontifications

* This site, rolandtanglao,com, uses a command line static website generator called ```jekyll``` written in ruby which generates HTML which I then upload to the free static website hosting service ```surge.sh```
* This is great **for me**. Since command lines, ruby et al are my friends since 1984 :-) ! (i first used the Unix command line in 1984 or maybe a year or 2 earlier not sure!)
* But it's dumb, why couldn't I do this in a web browser?
* Make it so lazy web :-)
* Anyhow this isn't an original idea. 
* Dave Winer's been riffing on this for ages and [here's a quote from his most recent thinking on browser static site generation plus uploading to static site cloud hosting](http://scripting.com/2017/01/05/itsTimeToThinkOfTheUsers.html):

**QUOTE**

<blockquote>

Here's a sketch of how the service would work.<br />

   1. Start with a user-facing service like Dropbox, Google Drive, Amazon Cloud Drive. <br />
    
   2. Add an API that allows a JavaScript app running in the browser to write into a folder in a user's space. The user grants access via oAuth, as they do with Twitter, Facebook, etc. <br />
    
   3. Connect to a registrar to allow a user to associate a domain name with a folder. Or map a domain they register elsewhere. A revenue opportunity.
</blockquote>

**END QUOTE**