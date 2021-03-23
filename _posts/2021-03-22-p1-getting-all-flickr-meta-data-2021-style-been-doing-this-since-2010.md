---
layout: post
title: "How To retrieve flickr photos meta data in a 2021 Stylee! Been doing this since September 2010! Now with Ruby 3.0 'except'"
---
* I started using the flickr API in September 2010: See [getGastownPhotos](https://gist.github.com/rtanglao/571353).rb! 11 years can you believe it?!?

* Here's how I do it in 2021! 

  * Use [Ruby 3.0 with the new `Hash#except` method](https://bigbinary.com/blog/ruby-3-adds-new-method-hash-except) to exclude members of a hash table in order to [flatten](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/backup-RolandsPublicPhotoMetaDataByYear.rb#L123) a json structure so it can be converted to CSV.

  * Output is CSV not mongodb so it can be used in R and converted to SQLite:

    * My [2020 flickr photo metadata](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/2020-roland-flickr-metadata.csv)
    * My [2019 flickrphoto metadata](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/2019-roland-flickr-metadata.csv)

## Some technical details

* You will of course need your flickr api key which you can find at:
    * `https://www.flickr.com/services/apps/by/<yourid>`
* [`backup-RolandsPublicPhotoMetaDataByYear.rb`](https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/backup-RolandsPublicPhotoMetaDataByYear.rb) flattens the JSON output from the flickr API. Luckily there's only 1 thing that has to be flattened which is:
* `photo["description"]["_content"]` which is flattened to `photo["description_content"]`

```bash
bundle install
bundle exec ./backup-RolandsPublicPhotoMetaDataByYear.rb 2020 # output: 2020-roland-flickr-metadata.csv
bundle exec ./backup-RolandsPublicPhotoMetaDataByYear.rb 2019 # output: 2019-roland-flickr-metadata.csv
```

