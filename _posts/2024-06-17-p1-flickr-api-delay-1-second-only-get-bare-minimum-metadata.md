---
layout: post
title: "Lessons learned: Flickr API limit of 1 API request / second means running 12 threads in parallel then I need to delay at least 1 second between API requests (assuming my code needs 1 second to do its thing) and get the bare minimum metadata & flickr ids are larger than ruby max int which breaks ruby sorting"
---
* Lessons learned from [my super long flickr average colour thread on Mastodon](https://devdilettante.com/@roland/112456929894572722):  Lessons learned: Flickr API limit of 1 API request / second means that if I am running 12 threads in parallel then I need delay minimum of 1 second between API requests (assuming my code needs 1 second to do its thing) and get the bare minimum metadata.
* I also learned that flickr integer ids are bigger than the maximum ruby ids so sorting by flickr ids as integers does NOT work. Oops :-)

### Thread

1. 1 of whenever I get bored or give up (OWIGBOGU)  :-) [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour My next project I guess is hourly average colour of all of flickr hmmmm :-)

2. 2/OWIGBOGU :-) [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour i wonder how many photos are uploaded hourly? 100,000? more? less?

3. 3/OWIGBOGU :-) [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour I am sure that 50% of  photos are uploaded many hours after they are  taken. Possibly more. Also the flickr API might not give me all the  photos. So I guess I'll think of it as an hourly snapshot of world wide  flickr average colour :-)

4. 4/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour And it will be line noise in appearance :-) with no real patterns of colour I think which has become mundane for me :-) Mundane world wide average colour hourly for the win :-)

5. 5/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour maybe store the average colours of photos as ints? 
   `magick -list Storage`
   output:
```
   Char
   Double
   Float
   Long
   LongLong
   Quantum
   Short
```
6. 6/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour gave up on `imagemagick` stream because i couldn't get it to work. Same with `vips`: too complicated. Going with :`magickimp = sprintf("magick convert \"%s\" -resize 1x1 txt:- | ggrep -Po \"#[[:xdigit:]]{6}\"", filename.gsub(/\$/, '\$'))` from https://github.com/rtanglao/rt-flickr-sqlite-csv/blob/main/get-filename-imagemagick-average-colour-from-75x75thumbnail.rb See also: [http://rolandtanglao.com/2021/04/05/p](http://rolandtanglao.com/2021/04/05/p1-rename-file-from-rgb-to-raw-opened-photoshop-converted-to-png/)
7. 7/OWIGBOGU #rt-flickr-worldwide-average-colour I think my current plan is:
   1\. use the flickr api to get all the metadata for an hour
   2\. download the first 10,000 75 pixel by 75 pixel thumbnails (maybe I'll download all teh meta data but only 10,000 thumbs?!?)
   3\. Make a 100 by 100 average colour graphic (or maybe 200 x 200 if I decide to download the first 40,000 thumbnails instead of the the first 10, 000)
8. 8/OWIGBOGU #rt-flickr-worldwide-average-colour It turns out I have most of the code I need in getLastFewWorldWidePhotos.rb , https://github.com/rtanglao/rt-flickr-worldwide-barcode/blob/main/getLastFewWorldWidePhotos.rb <-- That code plus the resize from post #6 in this thread is all I need I think :-) Famous last words.
9. 9/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour I'm going to attempt to do a vertical bar graph style for each hour. Current plan:
   1. store the thumbnails in a daily directory e.g. THUMBS/2024-05-19
   2. store all the flickr metadata in a metadata directory e.g. "METADATA"
10. 10/OWIGBOGU #rt-flickr-worldwide-average-colour It looks like there's approximately 24000 photos uploaded to flickr every hour. Less than I thought. From my WIP at: https://github.com/rtanglao/rt-worldwide-average-colour/blob/main/get-thumbs-for-1hour-and-make-vertical-infographic.rb
    `[1] pry(main)> photos = photos_on_this_page['photos'] => {"page"=>1,  "pages"=>48, "perpage"=>500,"total"=>23505...`
11. 11/OWIGBOGU #rt-flickr-worldwide-average-colour going for it :-) `parallel ./get-metadata-for-1-hour.rb 2024 1 1 {} ::: 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23`
12. 12/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour the metadata file for 1 hour is over 20 Megabytes LOL :-)
13. 13/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour December 25, 2023 is even more hilarious. 194, 500 photos in 1 hour :-)
```
    -rw-r--r--  1 roland  staff   224M 21 May 07:20 2023-12-25-00-flickr-metadata.csv
    roland@Rolands-MacBook-Pro METADATA % mlr --csv count 2023-12-25-00-flickr-metadata.csv 
    count
    194500
```
14. 14/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour where's the best place to store these huge metadata files :-) ??!?  dropbox? S3? don't bother :-) ?!? i am leaning towards not bothering :-)
15. 15/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour 215,000 photos uploaded in 1 hour on Christmas day 2023. [#SillyStats](https://devdilettante.com/tags/SillyStats) :-)
```
    % find . -name '*.csv' -print | xargs -n 1  mlr --csv count
    count
    187500
    count
    189000
    count
    197000
    count
    189500
    count
    202500
    count
    207000
    count
    187000
    count
    203500
    count
    198000
    count
    198000
    count
    210500
    count
    197000
    count
    205500
    count
    191000
    count
    195000
    count
    194500
    count
    202500
    count
    199000
    count
    215000
    count
    206000
    count
    202500
    count
    199500
    count
    199500
    count
    201000
```

16. 16/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour
    so I think I will code something like `if > 200K photos pick 4000 random ones else pick number of photos / 200 K * 4000`

17. 17/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour the following seems to be working `parallel --jobs 3 --results LOGS  ../../generate-hourly-info-graphic.rb ::: *.csv`
    code: [generate-hourly-info-graphic.rb](https://github.com/rtanglao/rt-worldwide-average-colour/blob/main/generate-hourly-info-graphic.rb)

18. 18/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour `magick montage "2023-12-25*.png" -tile 24x1  -geometry "+0+0"   daily-random-4000-2023-12-25.png`. On flickr: https://flic.kr/p/2pTMVQZ

19. 19/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour The default `gravity` setting of `Center` is not what we want :-) Use  `South` to align all images with the bottom of the image https://imagemagick.org/discourse-server/viewtopic.php?t=21965 `magick montage "2023-12-25*.png" -tile 24x  -gravity South -geometry "1x4000+0+0"  daily-random-4000-2023-12-25.png`

20. 20/OWIGBOGU [#rt](https://devdilettante.com/tags/rt)-flickr-worldwide-average-colour flickr ids e.g. 53733918346 are greater than ruby's maximum integer value so the sort method fails if you are sorting using flickr's ids converted to integers.:

    `53733918346 > 2147483647 => true`
    Solution: sort using a string I guess :-) !?!?

21. 21/OWIGBOGU #rt-flickr-worldwide-average-colour https://github.com/rtanglao/rt-worldwide-average-colour/blob/main/sorted-asc-try2-generate-hourly-info-graphic.rb is the code to generate sorted ascending hourly graphics (instead of sorted randomly) command line:
 `../../sorted-asc-try2-generate-hourly-info-graphic.rb 2023-12-25-00-flickr-metadata.csv`
22. 22/OWIGBOGU #rt-flickr-worldwide-average-colour  generate hourly infographics each with up to 4000 photos randomly picked i.e. `y pixels x 1 pixel` where `y<=4000` sorted by ascending time:
`parallel --jobs 3 --results LOGS ../../sorted-asc-try2-generate-hourly-info-graphic.rb ::: *.csv `
23. 23/OWIGBOGU #rt-flickr-worldwide-average-colour  Let's get the metadata for all of December :-) 
`parallel --jobs 3 ./get-metadata-for-1-hour.rb 2024 12 ::: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 26 27 28 29 30 31 ::: 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23`
24. 24/OWIGBOGU #rt-flickr-worldwide-average-colour It's still running 7 hours later LOL. Optimization is in order perhaps? Because 24 hours / day *30 days *6 minutes per hour /60 minutes per hour = 72 hours :-)
25. 25/OWIGBOGU #rt-flickr-worldwide-average-colour  8 `performance cores` so let's try 8 jobs & see if that's faster. It might be but I think I'll need to kill it anyway because I'll need to move storage from the internal SSD to an external 1 to have enough space to hold the metadata files!
`parallel --jobs 8 ./get-metadata-for-1-hour.rb 2024 12 :::   3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 26 27 28 29 30 31 ::: 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 `
26. 26/OWIGBOGU #rt-flickr-worldwide-average-colour YAGNI :-) You Ain't gonna need it is an overused cliche but i am going to refactor the code to download only the necessary metadata and to check the flickr status code and to randomly delay between 500ms and 4 seconds to avoid the dreaded rate limit :-) EDIT:3600 queries per hour :-)
27. 27/OWIGBOGU #rt-flickr-worldwide-average-colour 
   * 3600 flickr api requests per hour
   * 300,000 photos / 500 photos per page = 600 API queries for each hour 600 * 24 = 600*24 = 14,400 api requests for 1 day
   * 14400 / 3600 = 4 hours of API request for each day, so sleep <del>0.25</del>4 seconds between API requests. Perhaps <del>1</del> 3 seconds is more than enough margin of error since it takes time to process each of the 500 photos?!?!?

​    

## Previously

* May 15, 2024: [feh --randomize is great for viewing random images; not great for making collages, use imagemagick instead](http://rolandtanglao.com/2024/05/15/p2-feh-great-for-randomly-displaying-images-not-for-collages-use-imagemagick-instead/)        