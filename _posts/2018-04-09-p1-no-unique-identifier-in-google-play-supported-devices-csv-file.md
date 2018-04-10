---
layout: post
title: "No unique identifier in Google Play's CSV file of supported devices"
---

## Pontifications

* Hilariously bad :-) : No unique identifier in Google Play's CSV file of supported devices
* Maybe Google has it but doesn't want to export it or maybe Android just doesn't have it due to a bad design decision at the beginning of Android? Maybe something else :-) ?!?
* Anyhow if I hash together all 4 fields: Retail Branding, Marketing Name, Device and Model, I do get something unique, hooray
* Here's the code from: [synthetic\_add\_device\_branding\_marketing\_model.rb](https://github.com/rtanglao/rt-fennec-gplay/blob/master/synthetic_add_device_branding_marketing_model.rb)  :

 
```ruby
id_hashstr = ""
id_hashstr +=  d1["Retail Branding"] if !d1["Retail Branding"].nil?
id_hashstr +=  d1["Marketing Name"] if !d1["Marketing Name"].nil?
id_hashstr +=  d1["Device"] if !d1["Device"].nil?
id_hashstr +=  d1["Model"] if !d1["Model"].nil?
d1["id"] = Digest::SHA2.new(256).hexdigest(id_hashstr)
```