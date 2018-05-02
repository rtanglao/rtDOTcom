---
layout: post
title: "How to invoke Chromedriver from Windows Subsystem for Linux for Selenium (should work with Firefox too) from Stack Overflow:  Using BashOnWindows with Selenium? #1169 "
---

## Pontifications

* Makes me want to get a real Linux machine where these kludges aren't necessary :-) i.e. WSL is a gateway drug to using real Linux! 
* From [Using BashOnWindows with Selenium? #1169](https://github.com/Microsoft/WSL/issues/1169#issuecomment-293023930)  

**QUOTE**

<blockquote>

With the regular Windows environment, in my Python script I'd normally have:<br /><br />

webdriver.Chrome()<br /><br />

This works as I've added c/Python34/Scripts/ in my path (which is where I placed chromedriver.exe<br /><br />

...<br /><br />

Unfortunately, most Linux tools think that chromedriver and chromedriver.exe are different executables :-)<br /><br />

One possible workaround (I haven't tried it myself): You could create a text file /mnt/c/Python34/Scripts/chromedriver and populate it with the following:<br /><br />

#!/bin/sh<br />
chromedriver.exe "$@"<br /><br />

</blockquote>

**END QUOTE**

