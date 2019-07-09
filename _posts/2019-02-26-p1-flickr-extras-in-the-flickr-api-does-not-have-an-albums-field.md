---
layout: post
title: "When you get a flickr photo using the search API or the photoset API, you can't determine which photoset it is in by setting a field in extras"
---

# Pontifications

* [When you get a flickr photo using the search API or the photoset API, you can't determine which photoset the photo is by setting a field in extras](http://code.flickr.net/2008/08/19/standard-photos-response-apis-for-civilized-age/)
* Therefore I think it's best to add a field e.g. ```synthetic_photos_sets_array``` which is an array of photoset ids that this photo belongs to.
* Interestingly enough , the certificate for code.flickr.net is broken so here is the 2008 (! still works in 2019!) blog post content for posterity's sake (and when the cert 100% breaks)

```
Funny story. I went to write a blog post and when the time came to link to the documentation of our standard “standard photos response” structure, I found we had never documented it!

Okay. Maybe that wasn’t so funny.

But anyway, this is the blog post before that other blog post, so that when I write that other blog post I’ve got something to point to.

And besides you should know this stuff if you’re using the API. It’s good stuff.
Standard Photos Response

The standard photos response is a data structure that we use when we want to return a list of photos. Most prominently the ever popular swiss-army-API flickr.photos.search() uses it, but also methods like flickr.favorites.getList() or flickr.groups.pools.getPhotos().

Beyond a common structure that gets serialized across all our different API response formats, standard photos response methods share a common set of arguments for sorting and paging (after all these are lists of photos), and the special extras argument.
Standard Photo Response, the XML Serialization

You’re basic standard photos response looks like this. It’s just an envelope for delivering a list of photos.

<rsp stat="ok">
  <photos page="1" pages="7" perpage="100" total="608">
    <photo id="2777191844" owner="51035734193@N01" secret="653a19d017" server="3059" farm="4" title="FAIL" ispublic="1" isfriend="0" isfamily="0"/>
    <photo id="2771521705" owner="51035734193@N01" secret="1878507379" server="3178" farm="4" title="In the street" ispublic="1" isfriend="0" isfamily="0"/>
  </photos>
</rsp>

We’ve got the standard Flickr <rsp> root element, a <photos> container describing the full list and the page we’re on, and some <photo> elements that include everything we need to display a photo.

Another largely undocumented deep structure in the Flickr API is a distinction between getList() and getInfo() methods. We tend to return a pared down list of identifiers, and provide methods for getting more info about individual items. Generally it’s a very useful pattern, and saves us all bandwidth, processing, and data rot.

However sometimes (often?) you’re wanting to display a bunch of photos, and having to roundtrip to call flickr.photos.getInfo() for every single one of them is annoying. (not to mention slow, and likely to get you frowned upon by our ops team)

That’s where extras come in. The idea behind extras is you can selectively enrich the bare bones list I showed you earlier with the metadata you need to display your bunch of photos, without the round trip, and without fetching more then you’ll need.

There are currently 13 different extras available, and we add new ones periodically as new concepts come online, or you make a compelling enough case for them.

As of today they are: license, date_upload, date_taken, owner_name, icon_server, original_format, last_update, geo, tags, machine_tags, o_dims, views, media.
license

Is the photo “All rights reversed”? Licensed under one of the CC license?

<photo id="2777191844" owner="51035734193@N01" secret="653a19d017"
 server="3059" farm="4" title="FAIL" ispublic="1" isfriend="0" isfamily="0" 
 license="3"/>

license=”3” means Attribution-NonCommercial-NoDerivs, you can get our mappings with flickr.photos.licenses.getInfo().
date_upload, date_taken, last_update

When was the photo uploaded to Flickr? When do we think it was taken? When was its metadata last twiddled?

<photo id="2772368826" owner="51035734193@N01" secret="1078392104"
 server="3122" farm="4"       title="Finger on the button" ispublic="1" isfriend="0" isfamily="0"
 license="3"  dateupload="1219006901" datetaken="2008-08-17 12:38:06" 
datetakengranularity="0"     lastupdate="1219117103"/>

Yes the extras param is called date_upload the attribute is dateupload, what can I say, legacy. Notice also that dateupload and lastupdate are epoch seconds, while datetakengranularity is probably best ignored.
owner_name and icon_server

Everything you need to properly credit the photographer, including their name, and the info necessary to display their buddyicon.

<photo id="2772368826" owner="51035734193@N01" secret="1078392104" 
server="3122" farm="4" title="Finger on the button" ispublic="1" isfriend="0" isfamily="0" 
ownername="kellan" iconserver="54" iconfarm="1"/>

geo

If the photo was geotagged include the latitude, longitude, and accuracy of the geotagging.

<photo id="2772368826" owner="51035734193@N01" secret="1078392104" 
server="3122" farm="4" title="Finger on the button" ispublic="1" isfriend="0" isfamily="0" 
latitude="40.714666" longitude="73.957333" accuracy="16"/>

tags and machine_tags

Note these are the “clean” versions of the tags and machine tags, which means spaces, and most punctuation will have been stripped.  Safe to display in HTML, and useable as URL fragments.

<photo id="2772368826" owner="51035734193@N01" secret="1078392104" 
server="3122" farm="4" title="Finger on the button" ispublic="1" isfriend="0" isfamily="0" 
tags="nyc streetart williamsburg ph:camera=iphone3g" 
machine_tags="ph:camera=iphone3g"/>

original_format and o_dims

Assuming you’re making API calls as a member who is authorized to download a photo (e.g. the photographer) you can ask for details about the unmodified, full resolution photo that was uploaded.  Get the original file format, the secret needed to construct the URL to the photo, and what the original’s dimensions are.

<photo id="2772368826" owner="51035734193@N01" secret="1078392104" 
server="3122" farm="4" title="Finger on the button" ispublic="1" isfriend="0" isfamily="0" 
originalsecret="xxxxxxxx" originalformat="jpg" o_width="1200" 
o_height="1600"/>

views

How many times has this photo been viewed by folks other then the person who uploaded it?

<photo id="2772368826" owner="51035734193@N01" secret="1078392104" 
server="3122" farm="4" title="Finger on the button" ispublic="1" isfriend="0" isfamily="0" 
views="9"/>

media

Is it a photo? Or a video? Has it been processed and is it ready for displaying? (media_status is a lot more useful for videos)

<photo id="2771521705" owner="51035734193@N01" secret="1878507379" 
server="3178" farm="4" title="In the street" ispublic="1" isfriend="0" isfamily="0" 
media="photo" media_status="ready"/>

Wow. What a list. Really, what more could anyone ever want? (that’s rhetorical)
The punch line

That’s standard photos responses, and how to use extras (paging and sorting is left as an exercise to the reader). Mastering the format is the key to building both interesting and performant API applications. use the metadata, love the metadata, and ditch the round trip.

And now for the that next blog post I mentioned ….

```