---
layout: post
title: "Inspired by Darren and Derek, I created a real-time daily flickr worldwide barcode website using ruby, a rust static web server and ngrok"
---
*  tl;dr: ([Looking for work! Hire me](http://rolandtanglao.com/2023/01/04/p1-thank-you-element-matrix/) :-) !): I sample the last 50 photos uploaded to flickr every 30 seconds using the [flickr API](https://www.flickr.com/services/api/flickr.photos.search.html) and slice them into a 1px x 640px slice and concatenate those slices into a daily flickr worldwide barcode. Check it out at: <https://rytbarcode.ngrok.io/> userid:`barcodes` password: `rock2023` (change the `o` to zero i.e. `0`) ([flickr archive of the barcodes](https://www.flickr.com/photos/roland/albums/72177720305856040)) Big thanks to [ngrok](https://ngrok.com/) for the trial enterprise plan! ngrok is indeed "Online in 1 line"! Super great!

### Details

* Since I am [looking for work as a support engineer on apps and frameworks like Matrix, Firefox, Thunderbird, Drupal, etc.](http://rolandtanglao.com/2023/01/04/p1-thank-you-element-matrix/),  I have some spare time when my daily job search tasks are done.
* Ever since I made a [barcode](http://rolandtanglao.com/2011/04/25/penmachine-dodging-buses-barcode-video-and-html5-web-app/) for the fabulous Derek Miller (RIP, check out his website [penmachine.com](https://penmachine.com/)), I've always wanted to make a barcode for flickr.
* I dedicate this barcode to [Darren Barefoot](https://darrenbarefoot.com/), who has has been an inspiration to me and many others in the Vancouver tech community, and who wrote one of his many great blog posts about this back in 2011: [Darren Barefoot:I made my own movie bar code](https://darrenbarefoot.com/2011/03/06/i-made-my-own-movie-bar-code/)
* What is is it? I sample the 50 last uploaded photos every 30 seconds using the flickr API and slice them into a 1px x 640px slice and concatenate those slices into a daily flickr worldwide barcode
* Please check it out at: <https://rytbarcode.ngrok.io/> userid:`barcodes` password: `rock2023` (change the `o` to zero i.e. `0`) ([flickr archive of the barcodes](https://www.flickr.com/photos/roland/albums/72177720305856040)) Big thanks to ngrok for the trial enterprise plan! ngrok is indeed "Online in 1 line"! Super great! Thanks ngrok folks I don't know how long my enterprise trial will last but it should be up for a week or two after which maybe I will move to their hobbyist plan and/or another comparable service like [%ailscale](https://tailscale.com/) [Funnel](https://tailscale.com/blog/introducing-tailscale-funnel/). Not sure yet :-) 

### Pretentious colophon :-)

#### Ruby script
* I wrote a ruby script, [getLastFewWorldWidePhotos.rb](https://github.com/rtanglao/rt-flickr-worldwide-barcode/blob/main/getLastFewWorldWidePhotos.rb), to download the photos using the [flickr.photos.search API](https://www.flickr.com/services/api/flickr.photos.search.html) which has always been and continues to be amazing. Since I don't trust Github to be around longer than my blog, the code is at the end of this blog post.
* I run this script on a Raspberry Pi 400 running Debian bullseye as follows:
```bash
while :; do ./getLastFewWorldWidePhotos.rb ; sleep 30; done
```
* The script creates a daily barcode called `barcode/barcode.png` using the `rmagick` ruby gem (front end for the amazing [imagemagick](https://imagemagick.org/) which I've used for information visualization for [over a decade](http://rolandtanglao.com/2011/04/19/imagemagick-montage-on-4600-photos-running-for-36-hours-alternatives/)) to slice the the photos into 1 pixel by 640 pixel slice and then appends it to the daily barcode. 
    * There are never enough examples of rmagick and imagemagic so here's the ruby code fragment you need to append a 1 pixel slice to the daily barcode using `montage`:
```ruby
image_list = Magick::ImageList.new(DAILY_BARCODE_FILEPATH, BARCODE_SLICE)
    montaged_images = image_list.montage { |image| image.tile = '2x1', image.geometry = '+0+0' }
    montaged_images.write(DAILY_BARCODE_FILEPATH)
# 2x1 means 2 images horizontally i.e. 1. the current barcode 
# and 2. the barcode to append and  1 image vertically
# +0+0 means make the image at the origin not some funky default :-)
```
* It also keeps a copy of the daily barcode in a filed called `barcode/<yyyy/<mm>/<dd>/<yyyy>-<mm>-<dd>.png` e.g. for Feb 8 2023: `barcode/2023/02/08/2023-02-08.png`
* The script (and the entire system!) could be improved of course but hey it's my job to look for a job not to code this script! e.g. the exception handling, redundant checking File system checks, etc

### Rust static web server

* On the same Raspberry Pi 400, I run the [rust static webserver](https://github.com/static-web-server/static-web-server) and serve up `barcode.png`. Why rust? And this webserver? Just for fun really: Any static webserver would do :-) of course!
```bash
static-web-server --port 8080 --root ~/Documents/GIT/rtbarcodewebsite/ & 
```
* And I expose it to the world using ngrok:
```bash
ngrok http 8080 --subdomain rytbarcode --basic-auth=barcodes:passwordredacted
```
* The home page just [auto-refreshes](http://rolandtanglao.com/2023/02/07/p1-how-to-refresh-img-webpage-using-javascript/) the png every 5 seconds using `fetch()` in Javascript. The code is at the end of this page. Thanks [Yoric](https://yoric.github.io/) and [Brendan](https://brendan.abolivier.bzh/)!

### Previously
* February 7, 2023: [How To refresh an image in place on a web page using JavaScript](http://rolandtanglao.com/2023/02/07/p1-how-to-refresh-img-webpage-using-javascript/)
* February 5, 2023: [SoftCreatR's Imagemagick Easy install for Ubuntu and Debian aka 'imei' worked for me on my Raspberry Pi 400 running Debian bullseye](http://rolandtanglao.com/2023/02/05/p1-softcreatr-imagemagick-easy-install-ubuntu-debian-how-to/)
* December 10, 2022: [Tailscale Funnel is a reverse proxy service complete with TLS cert, DNS, public IP address and HTTPS server that seems perfect for small, experimental software on the internet like snac2](http://rolandtanglao.com/2022/12/10/p1-tailscale-funnel-ideal-for-home-hosted-experimental-software/)
* April 25, 2011: [penmachine dodging buses barcode video & HTML5 Web App](http://rolandtanglao.com/2011/04/25/penmachine-dodging-buses-barcode-video-and-html5-web-app/)
* April 20, 2011 [Penmachine barcode 1.1](http://rolandtanglao.com/2011/04/20/penmachine-barcode-1-1/)

### Ruby code: getLastFewWorldWidePhotos.rb
```ruby
#!/usr/bin/env ruby
# frozen_string_literal: true

require 'rubygems'
require 'bundler/setup'
require 'typhoeus'
require 'amazing_print'
require 'time'
require 'date'
require 'logger'
require 'io/console'
require 'parseconfig'
require 'fileutils'
require 'pry'
require 'pry-byebug'
require 'tzinfo'
require 'down/http'
require 'json'
require 'rmagick'

include Magick

def get_flickr_response(url, params, _logger)
  url = "https://api.flickr.com/#{url}"
  try_count = 0
  begin
    result = Typhoeus::Request.get(
      url,
      params: params
    )
    x = JSON.parse(result.body)
  rescue JSON::ParserError
    try_count += 1
    if try_count < 4
      logger.debug "JSON::ParserError exception, retry:#{try_count}"
      sleep(10)
      retry
    else
      logger.debug 'JSON::ParserError exception, retrying FAILED'
      x = nil
    end
  end
  x
end

logger = Logger.new($stderr)
logger.level = Logger::DEBUG

flickr_config = ParseConfig.new('flickr.conf').params
api_key = flickr_config['api_key']

TEN_MINUTES_IN_SECONDS = 60 * 10
BEGIN_TIME = Time.now.to_i - TEN_MINUTES_IN_SECONDS
logger.debug "BEGIN: #{BEGIN_TIME.ai}"
begin_mysql_time = Time.at(BEGIN_TIME).strftime('%Y-%m-%d %H:%M:%S')

extras_str = 'date_upload,url_l'

flickr_url = 'services/rest/'
logger.debug "begin_mysql_time:#{begin_mysql_time}"

NUM_PHOTOS_TO_DOWNLOAD = 50

url_params =
  {
    method: 'flickr.photos.search',
    media: 'photos', # Just photos no videos
    content_type: 1, # Just photos, no videos, screenshots, etc
    api_key: api_key,
    format: 'json',
    nojsoncallback: '1',
    extras: extras_str,
    sort: 'date-posted-desc',
    per_page: NUM_PHOTOS_TO_DOWNLOAD,
    page: 1,
    # Looks like unix time support is broken so use mysql time
    min_upload_date: begin_mysql_time
  }
photos_on_this_page = get_flickr_response(flickr_url, url_params, logger)
logger.debug "STATUS from flickr API:#{photos_on_this_page['stat']} num_pages:\
  #{photos_on_this_page['photos']['pages'].to_i}"
PARAMS_TO_KEEP = %w[id dateupload url_l height_l width_l]
photos = []
photos_on_this_page['photos']['photo'].each do |photo|
  # logger.debug "photo from API: #{photo.ai}"
  dateupload = Time.at(photo['dateupload'].to_i)
  logger.debug "dateupload:#{dateupload}"
  photo['id'] = photo['id'].to_i
  photo['dateupload'] = photo['dateupload'].to_i
  next if !photo.has_key?('height_l') || photo['height_l'] < 640 # Skip all photos that are less than 640px high.

  photo_without_unnecessary_stuff = photo.slice(*PARAMS_TO_KEEP)
  logger.debug "photo without unnecessary stuff: #{photo_without_unnecessary_stuff.ai}"
  photos.push(photo_without_unnecessary_stuff)
end
photos.sort! { |a, b| a['dateupload'] <=> b['dateupload'] }
# Get last photo and figure out the date for the Pacific timezone
# and skip prior dates (if there are any)
last = photos[-1]
tz = TZInfo::Timezone.get('America/Vancouver')
localtime = tz.to_local(Time.at(last['dateupload']))
localyyyy = localtime.strftime('%Y').to_i
localmm = localtime.strftime('%m').to_i
localdd = localtime.strftime('%d').to_i
startdate = tz.local_time(localyyyy, localmm, localdd, 0, 0).to_i
photos.reject! { |p| p['dateupload'] < startdate }
exit if photos.length.zero?
BARCODE_SLICE = '/tmp/resized.png'
HEIGHT = 640
WIDTH = 1
# Create barcode/yyyy/mm/dd directory if it doesn't exist
DIRECTORY = format(
  'barcode/%<yyyy>4.4d/%<mm>2.2d/%<dd>2.2d',
  yyyy: localyyyy, mm: localmm, dd: localdd
)
ID_FILEPATH = "#{DIRECTORY}/processed-ids.txt"
BARCODE_FILEPATH = 'barcode/barcode.png'
DAILY_BARCODE_FILEPATH = format(
  '%<dir>s/%<yyyy>4.4d-%<mm>2.2d-%<dd>2.2d.png',
  dir: DIRECTORY, yyyy: localyyyy, mm: localmm, dd: localdd
)
FileUtils.mkdir_p DIRECTORY
processed_ids = []
processed_ids = IO.readlines(ID_FILEPATH).map(&:to_i) if File.exist?(ID_FILEPATH)
photos.each do |photo|
  id = photo['id']
  next if processed_ids.include?(id)

  # Download the thumbnail to /tmp
  logger.debug "DOWNLOADING #{id}"
  # 640 height files shouldn't be more than 1 MB!!!
  retry_count = 0
  begin
    tempfile = Down::Http.download(photo['url_l'], max_size: 1 * 1024 * 1024)
  rescue Down::ClientError, Down::NotFound => e
    retry_count += 1
    retry if retry_count < 3
    next #raise(e) ie. skip the photo if we can't download it
  end
  thumb = Image.read(tempfile.path).first
  resized = thumb.resize(WIDTH, HEIGHT)
  resized.write(BARCODE_SLICE)
  if !File.exist?(DAILY_BARCODE_FILEPATH)
    FileUtils.cp(BARCODE_SLICE, DAILY_BARCODE_FILEPATH)
  else
    image_list = Magick::ImageList.new(DAILY_BARCODE_FILEPATH, BARCODE_SLICE)
    montaged_images = image_list.montage { |image| image.tile = '2x1', image.geometry = '+0+0' }
    montaged_images.write(DAILY_BARCODE_FILEPATH)
  end
  File.delete(tempfile.path)
  # After the thumbnail is downloaded,  add the id to the file and to the array
  # so we don't download it again!
  File.open(ID_FILEPATH, 'a') { |f| f.write("#{id}\n") }
  processed_ids.push(id)
  FileUtils.cp(DAILY_BARCODE_FILEPATH, BARCODE_FILEPATH)
end
```

#### HTML home page

```html
<!doctype html>
<html>
<!--
    Inspired by Darren Barefoot and Derek Miller. Thanks!
    http://rolandtanglao.com/2023/02/09/p1-worldwide-flickr-barcode
    https://darrenbarefoot.com/2011/03/06/i-made-my-own-movie-bar-code/
    Looking for work! Hire me: 
    http://rolandtanglao.com/2023/01/04/p1-thank-you-element-matrix/ :-) !
-->
<head>
<title>Worldwide Flickr Barcode</title>
<script>
async function loop() {
  // Our `<img>`.
  let img = document.getElementById("barcode");

  // The url of the data that we download. Initially, we haven't downloaded any data,
  // so `null`.
  let objectURL = null;

  while (true) {
    // Wait 5 seconds.
    await new Promise(resolve => setTimeout(resolve, 5000));

    // Get the data.
    let response = await fetch("https://rytbarcode.ngrok.io/barcode.png", { cache: 'no-cache' });

    // For images, we want the response as a blob (Binary Large Object)
    let blob = await response.blob();
    if (objectURL) {
      // If we already have data, clean up the memory.
      URL.revokeObjectURL(objectURL);
    }

    // Convert the blob into a URL.
    objectURL = URL.createObjectURL(blob);

    // ...and point the `<img>` to this image.
    img.setAttribute("src", objectURL); 
  }
}
</script>
</head>
<body>
<img id="barcode"/>
<script>loop();</script>
</body>
</html>

```