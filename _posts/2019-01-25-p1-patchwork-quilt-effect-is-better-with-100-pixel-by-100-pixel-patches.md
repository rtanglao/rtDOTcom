---
layout: post
title: "The 'patchwork quilt' effect that I'm looking for is better with 100 pixel by 100 pixel patches"
---
# Pontifications

* I've tried [5px x 1 px](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/oily-5px-zazzle-leg.rb), [10px by 10 px](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/oily-10x10px-zazzle-leg.rb) but I like 100 px by 100 px the best so far!

* Here's the code [oily-100x100px-zazzle-leg.rb
](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/oily-100x100px-zazzle-leg.rb):

```ruby
#!/usr/bin/env ruby
require 'json'
require 'rubygems'
require 'awesome_print'
require 'logger'
require 'vips'
require 'oily_png'

logger = Logger.new(STDERR)
logger.level = Logger::DEBUG

artofwhere_width =  3400
artofwhere_length = 6400
output_png =
  ChunkyPNG::Image.new(
    artofwhere_width, artofwhere_length,
    ChunkyPNG::Color::TRANSPARENT)
num_pixels = artofwhere_width * artofwhere_length

originals_from_flickr = []
ARGF.each_line do |file|
  image = Vips::Image.new_from_file file.chomp
  originals_from_flickr.push(image)
end
length = originals_from_flickr.length
logger.debug "number of flickr pics:" + length.to_s
#logger.debug files[0]
#logger.debug files[-1]
# 3400 / 10 px = 34 rows one way i.e. "horizontally"
# 6358 -> 6400 / 10 px = 64 rows the other way "vertically"
# each original is 4608 x 3456 px
# round down to 4600 x 3400 px

#     which means there are 46 ten pixel columns horizontally
#     and 34 ten pixel rows vertically

i = 0
x = 0
y = 0
loop do
  logger.debug "i:" + i.to_s
  if i > num_pixels
    break
  end
  xoffset = rand(0..45) * 100
  yoffset = rand(0..33) * 100
  flickr_pic = rand(0..length - 1)
  row_y = y
  (yoffset..yoffset + 99).each do |flickry|
    row_x = x
    (xoffset..xoffset + 99).each do |flickrx|
      #logger.debug "extract area:" + flickrx.to_s + "," + flickry.to_s
      r, g, b = originals_from_flickr[flickr_pic].getpoint flickrx, flickry
      output_png[row_x, row_y] = ChunkyPNG::Color.rgb(r.to_i, g.to_i, b.to_i)
      row_x += 1
    end
    row_y += 1
  end
  x += 100
  if x == artofwhere_width
    logger.debug "NEW ROW"
    x = 0
    y += 100
    next if y % 2 != 0
    interim_filename = sprintf("interim-100x100-oily-out-row-%4.4d.png", y-100)
    output_png.save interim_filename, :interlace => true
  end
  i += 10000
end
output_png.save "oily-100x100-out.png", :interlace => true

```

## Interim Output after 13 Rows

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/46153086474/in/datetaken-ff/" title="interim-100x100-oily-out-row-1300"><img src="https://farm8.staticflickr.com/7874/46153086474_6b25b4cc4a.jpg" width="266" height="500" alt="interim-100x100-oily-out-row-1300"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>