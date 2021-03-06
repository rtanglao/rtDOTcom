---
layout: post
title: '"Bug Adventures" II - Why doesn''t my GPS work?'
created: 1231130237
---
<p>
(Part 2 of my Bug Adventures series, for more real time wiki action check out my <a href="http://sites.google.com/site/bugadventures/">Bug Adventures wiki</a> where I flesh out my thoughts before posting them here!) 
</p>
<p>
<a href="http://bugcommunity.com/forums/viewtopic.php?p=1942#1942">Why doesn't my GPS aka BUGgps seem to work</a>?
By &quot;not working&quot;, I mean it doesn't get a GPS satellite lock which
results in a Java exception for those using the high level API and void
values e.g. &quot;$GPGLL,,,,,022837.595,V*1D &quot;for apps reading the RAW GPS
sentences.  My guess is it's a low level software bug that will be
fixed in the &quot;real soon now&quot; R1.4 software release. Note that I have
attached the external antenna and put it on the window sill where my
other GPSes (Nokia LD-4W, Nokia E71) have no problems obtaining a GPS
lock!
</p>
<p>
Herewith my debugging notes: 
</p>
<ol>
	<li><a href="http://bugcommunity.com/forums/viewtopic.php?t=351">http://bugcommunity.com/forums/viewtopic.php?t=351</a> seems to be the definitive source of how to fix your GPS! the fix in the thread:<br />
	<ol>
		<li>&quot;<span>navigate the front-panel menu to the GPS module
		and you will be able to see fix: True/False and IOX, which is the value
		of the IOX register:&quot;</span>
		<ol>
			<li><span>(front panel led sequence is: modules-&gt;GPS-&gt;IOX) I get 0x63 which means</span>
			<ol>
				<li><span>bit  0: 1 == no GPS fix, since fix is active low</span></li>
				<li><span>bit 1: 1 = no overcurrent condition</span></li>
				<li><span>bit 2: 0 = no wakeup from sleep</span></li>
				<li><span>bit 3: 0 = don't know what this is, guess is 0 means don't download firmware</span></li>
				<li><span>bit 4,5 unused</span></li>
				<li><span>bit 7,6 0,1 == external antenna<br />
				</span></li>
			</ol>
			</li>
		</ol>
		</li>
	</ol>
	</li>
	<li>Other people's code I have tried<br />
	<ol>
		<li>GPSRawFeedExample always outputs &quot;V*blah&quot; which I think means void!
		<ol>
			<li>e.g. $GPGLL,,,,,051302.397,V*10</li>
		</ol>
		</li>
		<li>GPSLoggerSimpleGUI - the GUI doesn't work but at least the program doesn't crash :-)</li>
		<li>GPSLogger2 creates a zero length file in /tmp but does nothing else e.g. /tmp/GPSSun Jan 04 20:25:49 UTC 2009.log</li>
		<li>GpsLogger_1.1 java.lang.NullPointerException<br />
		at com.buglabs.bug.module.gps.GPSModlet.getLatitudeLongitude(Unknown Source)</li>
		<li>My friend Simon's app has the same bug as GPS Logger 1.1 i.e. java.lang.NullPointerException<br />
		at com.buglabs.bug.module.gps.GPSModlet.getLatitudeLongitude(Unknown Source)
		<ol>
			<li>Simon's guess: the NMEA sentence they are getting from the underlying<br />
			hardware isn't quite in the format they expect, so they end up trying<br />
			to get a double out of the string  &quot;,&quot; </li>
			<li><a href="http://lists.buglabs.net/pipermail/bug-dev/2008-December/000167.html">http://lists.buglabs.net/pipermail/bug-dev/2008-December/000167.html</a> seems to be the same problem!</li>
		</ol>
		</li>
	</ol>
	</li>
	<li>Evidence that this is a Bug that's being worked on:
	<ol>
		<li>this fix went into  <span>svn</span> trunk (svn://svn.buglabs.net/bug/trunk  ) on December 14, 2008, <a href="http://svn.buglabs.net/svn/%21revision/7632">http://svn.buglabs.net/svn/!revision/7632</a><br />
		// default to passive (external) antenna, until<br />
		// such time as we have confidence in the internal            <br />
		// antenna's ability to obtain a fix          <br />
		log.log(LogService.LOG_DEBUG, &quot;GPSModlet defaulting to passive (external) antenna&quot;);              <br />
		setPassiveAntenna();        </li>
	</ol>
	</li>
</ol>
