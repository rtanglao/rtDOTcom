---
layout: post
title: We all make sh*tty software including M$crosoft part 8888 -- www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com
---

## Pontifications

* From [The worm that spreads WanaCrypt0r](https://blog.malwarebytes.com/threat-analysis/2017/05/the-worm-that-spreads-wanacrypt0r/) 

**QUOTE**

<blockquote>

The WinMain of this executable first tries to connect to the website www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com. It doesn’t actually download anything there, just tries to connect. If the connection succeeds, the binary exits.<br /><br />

This was probably some kind of kill switch or anti-sandbox technique. Whichever it is, it has backfired on the authors of the worm, as the domain has been sinkholed and the host in question now resolves to an IP address that hosts a website. Therefore, nothing will happen on any new systems that runs the executable. This only applies to the binary with the hash listed above; there may well be new versions released in the future. UPDATE: The second argument to InternetOpenA is 1 (INTERNET_OPEN_TYPE_DIRECT), so the worm will still work on any system that requires a proxy to access the Internet, which is the case on the majority of corporate networks. Thanks to Didier Stevens for spotting what was missed by most.

</blockquote>

**END QUOTE**
