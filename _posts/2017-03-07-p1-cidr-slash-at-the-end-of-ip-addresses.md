---
layout: post
title: What does the CIDR slash notation mean in IP addresses e.g. 63.245.214.128/26 ?
---

## Pontifications

Classless Inter Domain Routing aka CIDR notation means you have to apply a bit mask for the number of bits after the slash so in our example 63.245.214.128/26 that means 26 bit bit mask. 

* ```# of valid IP addresses 2^(32-n)``` where "n" is the number after the slash
* 63.245.214.128/26 = 2^(32-26) = 2^6 = 64 valid IP addresses 
    * which are: 63.245.214.128 to 63.245.214.191
* More info:
    * [https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation)
    * [https://en.wikipedia.org/wiki/IP_address](https://en.wikipedia.org/wiki/IP_address)
    * [cidr range to ip address range converter](http://www.ipaddressguide.com/cidr#range)


