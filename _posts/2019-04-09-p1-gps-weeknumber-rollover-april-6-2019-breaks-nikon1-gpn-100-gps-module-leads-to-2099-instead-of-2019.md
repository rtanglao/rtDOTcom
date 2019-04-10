---
layout: post
title: "Nikon 1 GPS GP-N100 erroneously sets the EXIF in photos to 2099 instead of 2019 due to a GPS Week rollover bug starting April 6, 2019"
---

# Pontifications

* The [Nikon 1 GPS GP-N100 module](https://www.nikonusa.com/en/nikon-products/product/gps/gp-n100-gps-unit.html#tab-ProductDetail-ProductTabs-Overview) for Nikon 1 cameras erroneously sets the EXIF in photos to the year 2099 instead of 2019 due to a [GPS Week rollover](https://en.wikipedia.org/wiki/Time_formatting_and_storage_bugs#Second_GPS_rollover) that happened on April 6, 2019 ([and other GPS modules have the same bug](https://gpsd-dev.berlios.narkive.com/XGU31nJE/gps-date-fail-due-to-week-counter-rollover-not-a-gpsd-bug))
