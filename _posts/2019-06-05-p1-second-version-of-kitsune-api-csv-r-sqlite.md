---
layout: post
title: "rt-kits-api2 second version of my SUMO API code, now with daily CSV :-)"
---

# Pontifications

* [rt-kits-api2](https://github.com/rtanglao/rt-kits-api2) is the second version of my KITSUNE API code (first version was [https://github.com/rtanglao/rt-kitsune-api/]( https://github.com/rtanglao/rt-kitsune-api/ ) )
* Instead of MongoDB,  I'll use one CSV file per UTC day (daily CSV files for: [June 2019](https://github.com/rtanglao/rt-kits-api2/tree/master/201906), [May 2019](https://github.com/rtanglao/rt-kits-api2/tree/master/201905)) which will allow easy importing into R, SQLite etc
