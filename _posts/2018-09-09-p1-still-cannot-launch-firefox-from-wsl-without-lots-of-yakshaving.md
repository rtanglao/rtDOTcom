---
layout: post
title: "Still can't launch Firefox from Windows Subystem From Linux without a Selenium server and some hacks that nobody has working (Chrome works though)"
---

## Pontifications

* Still can't launch Firefox from Windows Subystem From Linux without a Selenium server and some hacks that nobody has w	working (Chrome works though)
	* above according to [browser\_testing\_on\_wsl by danwhitston](https://gist.github.com/danwhitston/5cea26ae0861ce1520695cff3c2c3315):
	
<blockquote>
	
	The problem with browser testing in WSL is that it relies on opening and controlling a web browser, and browsers don’t work on WSL at present as it deliberately doesn’t include X Windows or some other GUI manager - it’s meant to be command line after all. So while you can apt-get firefox, trying to actually run it isn’t going to work.<br /><br />
	
	...<br /><br />
	
	For Firefox (incomplete)<br /><br />

    Install geckodriver on Windows. Note that the modern webdriver for Firefox is now known as Marionette, but that, if I understand correctly, the old webdriver is used for remote connections such as the one we're setting up.<br /><br />

    Try something similar to the Chrome code below, but with :firefox instead of :chrome<br /><br />

    Get errors such as 'Selenium::WebDriver::Error::UnknownError: The path to the driver executable must be set by the webdriver.gecko.driver system property' and try Chrome instead<br /><br />

</blockquote>
	
* Oh well maybe I'll eventually find the time to make it work with Firefox!
* In the meantime I wrote [open-day-in-browser.rb](https://github.com/rtanglao/rt-kitsune-api/blob/master/open-day-in-browser.rb) which only works on Mac and not on WSL! Someday!
	