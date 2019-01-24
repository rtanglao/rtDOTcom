---
layout: post
title: "Did you catch the bug in yesterday's vips code? I've coded an oily_png version that is at least twice as fast!"
---
# Pontifications

* Did you catch the bug in  [yesterday's vips code to create random 5x5 images from my Mozlando Space Shuttle Atlantis pics](http://rolandtanglao.com/2019/01/22/p1-which-is-faster-at-creating-png-images-imagemagick-convert-oilypng-ruby-vips/), [vips-create5x5-zazzle-leg.rb](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/vips-create5x5-zazzle-leg.rb)? It was the ```x+=5``` line!
* The bug will cause only every 5th pixel to be written out, so I will let it run without fixing the bug, might be a nice pattern.
* Here is today's code, [oily-5px-zazzle-leg.rb](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/oily-5px-zazzle-leg.rb)

```ruby
#!/usr/bin/env ruby
require 'json'
require 'rubygems'
require 'awesome_print'
require 'time'
require 'date'
require 'logger'
require 'vips'
require 'oily_png'

logger = Logger.new(STDERR)
logger.level = Logger::DEBUG

artofwhere_width = 3325
artofwhere_length = 6360
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
# 3325 / 5 px = 665 rows one way i.e. "horizontally"
# 6358 -> 6360 / 5 px = 1272 rows the other way "vertically"
# each original is 4608 x 3456 px
# round down to 4605 x 3455 px

#     which means there are 921 five pixel columns horizontally
#     and 691 five pixel rows vertically

# which means the script needs to pick 847210 (665 * 1274) random 5px x 5x patches
i = 0
x = 0
y = 0
loop do
  i += 5
  logger.debug "i:" + i.to_s
  if i > num_pixels
    break
  end
  xoffset = rand(0..920) * 5
  yoffset = rand(0..690) * 5
  flickr_pic = rand(0..length - 1)
  (xoffset..xoffset + 4).each do |flickrx|
    r, g, b = originals_from_flickr[flickr_pic].getpoint flickrx, yoffset
    output_png[x, y] = ChunkyPNG::Color.rgb(r.to_i, g.to_i, b.to_i)
    x += 1
  end
  if x > 920
    logger.debug "NEW ROW"
    x = 0
    y += 1
  end
end
output_png.save "oily-out.png", :interlace => true

```