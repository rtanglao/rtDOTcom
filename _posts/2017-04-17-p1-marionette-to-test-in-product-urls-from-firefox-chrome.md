---
layout: post
title: Mozilla Marionette to test in-product URLs from Firefox chrome
---

## Pontifications

* Note to self: Use [Mozilla Marionette](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette) to test in-product URLs from Firefox for desktop (and Android) chrome

FROM the afore linked MDN page:

**QUOTE**

<blockquote>
"Marionette is an automation driver for Mozilla's Gecko engine. It can remotely control either the UI or the internal JavaScript of a Gecko platform, such as Firefox. It can control both the chrome (i.e. menus and functions) or the content (the webpage loaded inside the browsing context), giving a high level of control and ability to replicate user actions. In addition to performing actions on the browser, Marionette can also read the properties and attributes of the DOM.<br /><br />


If this sounds similar to Selenium/WebDriver then you're correct! Marionette shares much of the same ethos and API as Selenium/WebDriver, with additional commands to interact with Gecko's chrome interface. Its goal is to replicate what Selenium does for web content: to enable the tester to have the ability to send commands to remotely control a user agent."
</blockquote>
**END QUOTE**