---
layout: post
title: "To get more of a patchwork quilt effect I'm trying 200x200px"
---
# Pontifications

* Yesterday's 100px by 100px was great but to get more of a patchwork quilt effect, I'm trying 200px by 200px as well!
* Here's the code, [oily-200x200px-zazzle-leg.rb](https://github.com/rtanglao/rt-mozlando2018-ksc/blob/master/oily-200x200px-zazzle-leg.rb):

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

# 3400 / 200 px = 17 rows one way i.e. "horizontally"
# 6358 -> 6400 / 200 px = 32 rows the other way "vertically"
# each original is 4608 x 3456 px
# round down to 4600 x 3400 px

#     which means there are 23 two hundred pixel columns horizontally
#     and 17 two hundred pixel rows vertically

i = 0
x = 0
y = 0
num_rows = 0
loop do
  logger.debug "i:" + i.to_s
  if i >= num_pixels
    break
  end
  xoffset = rand(0..22) * 200
  yoffset = rand(0..16) * 200
  flickr_pic = rand(0..length - 1)
  row_y = y
  (yoffset..yoffset + 199).each do |flickry|
    row_x = x
    (xoffset..xoffset + 199).each do |flickrx|
      #logger.debug "extract area:" + flickrx.to_s + "," + flickry.to_s
      r, g, b = originals_from_flickr[flickr_pic].getpoint flickrx, flickry
      output_png[row_x, row_y] = ChunkyPNG::Color.rgb(r.to_i, g.to_i, b.to_i)
      row_x += 1
    end
    row_y += 1
  end
  x += 200
  if x == artofwhere_width
    logger.debug "NEW ROW"
    x = 0
    y += 200
    num_rows += 1
    next if num_rows % 2 == 0
    t = Time.now
    interim_filename = sprintf(
      "%4.4d-%2.2d-%2.2d-%2.2d-%2.2d-interim-200x200-oily-out-row-%4.4d.png", \
      t.year, t.month, t.day, t.hour, t.min,
      y-200)
    output_png.save interim_filename, :interlace => true
  end
  i += 40000
end
t = Time.now
filename = sprintf("%4.4d-%2.2d-%2.2d-%2.2d-%2.2d-oily-200x200-out.png",
  t.year, t.month, t.day,  t.hour, t.min)
output_png.save filename, :interlace => true

```