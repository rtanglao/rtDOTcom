---
layout: post
title: Tried to upgrade Bug Labs Bug Root FS to R1.4 but now my BUG is borked
created: 1237182255
---
<p>On Wednesday, the official release of Bug Labs R1.4 came out. <strong>Summary</strong>: I tried to upgrade my Bug Root File System, and my Bug no longer works and I am not sure where to document my problem (should I put it on the wiki or the forums?). I guess I will get on good 'ole IRC to get this fixed on Monday (I really dislike IRC, it reminds of the 1990s, full of people trying to help you but no RSS feed, no archives without bots that require Kevin Marks level knowledge to keep them up and running, and no distillation of knowledge so you are doomed to explain the same things over and over again!). Help! If you can help, twitter me @rtanglao or email me roland AT rolandtanglao or I'll try to get help on IRC as well as post on the <a href="http://community.buglabs.net/bcruskie/posts/96-BUG-Release-1-4-and-SDK-1-2-8-1-are-now-live-#comment_121">Bug Labs R1.4 thread on community.buglabs.net</a>. Anybody who helps me, gets a free beer the next time they are in Vancouver (how about a Bug Labs meetup at <a href="http://openwebvancouver.ca/">Open Web 2009 in June 11-12 in Vancouver</a>?) Read on for all details.</p>
<h2>Details</h2>
<p>R1.4 = Bug Labs SDK 1.81 + Root FS 1.4 + Kernal 1.4 (Suggestion to Bug Labs: bundle these together or tag future releases so that tag 1.5 for example is the same release tag for SDK, FS and Kernal)</p>
<p>The Bug Labs documentation and web presence is confusing even for somebody like me who has been developing software for 20 years and uses confusing open source software like git and Drupal so that's saying something! And Bug Labs seems to admit it in this blog post from December, "<a href="http://community.buglabs.net/bballantine/posts/38-Finding-BUG-Tutorials-and-Documentation">Finding BUG Tutorials and Documentation</a>". My off-the-cuff recommendation given my developer relations experience at Nortel&nbsp;&nbsp;would be to create a single wiki page "Busy Developer's Guide to writing software for the BUG" (BDGB) with the bare minimum of info that is always up to date and to have the dev relations person (Alicia?) post a blog post on bugblogger.com whenever the BDGG is updated! Anyways...</p>
<h2>Here's what I did:</h2>
<p>Tried to upgrade my Root FS to R1.4 using the Mac instructions from <a href="http://bugcommunity.com/wiki/index.php/Update_your_BUG_memory_card" rel="nofollow">HOW to upgrade ROOT FS aka "Update your BUG memory card"</a> (see "Yak Shaving" section below for full details)</p>
<h2>Here's what happened:</h2>
<p>The Root FS upgrade appeared to work but when I boot the Bug it doesn't come up and doesn't activate the Ethernet over USB so I can't ssh in to check things out.</p>
<h2>Here's what I expected:</h2>
<p>I expected it to "just work" and then I could proceed to upgrading the kernal to R 1.4</p>
<h2>Guesses as to what went wrong</h2>
<ol>
  <li>A bug in the Root FS image?</li>

  <li>A bug in the <a href="http://sourceforge.net/projects/ext2fsx/">ext2fsx</a> software that I used namely 1.4d4</li>

  <li>Something else?</li>
</ol>
<h2>Yak Shaving (or what I did in exquisite detail)</h2>(<a href="http://gist.github.com/raw/79628/fc0994b620eda8b36ff741cfa85d4f87e81aadc0/gistfile1.sh">raw gist is here</a>)
<pre style="word-wrap: break-word; white-space: pre-wrap;">
dd if=/dev/disk1s1 of=BUG_backup.ext3.bin 
tar xvfjv bug-image-production-bug-R1.4-rootfs.ext3.bz2
dd if=bug-image-production-bug-R1.4-rootfs.ext3.bz2  of=/dev/disk1s1
95105+1 records in
95105+1 records out
sudo /usr/local/sbin/fsck.ext3  /dev/disk1s1
e2fsck 1.39 (29-May-2006)
Couldn't find ext2 superblock, trying backup blocks...
/usr/local/sbin/fsck.ext3: Bad magic number in super-block while trying to open /dev/disk1s1
The superblock could not be read or does not describe a correct ext2
filesystem.  If the device is valid and it really contains an ext2
filesystem (and not swap or ufs or something else), then the superblock is corrupt, and you might try running e2fsck with an alternate superblock:
    e2fsck -b 8193 &lt;device&gt;
sudo /usr/local/sbin/resize2fs  /dev/disk1s1
resize2fs 1.39 (29-May-2006)
/usr/local/sbin/resize2fs: Bad magic number in super-block while trying to open /dev/disk1s1
Couldn't find valid filesystem superblock.
</pre>
