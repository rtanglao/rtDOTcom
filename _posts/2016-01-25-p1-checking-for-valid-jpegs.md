---
layout: post
title: Using identify in ruby to determine if a JPEG is valid
---
So I don’t forget how to identify valid JPEGS using GraphicMagick’s identify (from [getTopColour.rb](https://github.com/rtanglao/rtgram/blob/master/getTopColour.rb)).

Notes:

1. graphicsmagick is mac only and supposedly faster, imagemagick is fine so on a non mac i.e. Linux comment out those three lines starting with “MiniMagick.configure”
2. I wonder if a pure ruby solution would work better?

``` ruby
require 'mini_magick'

MiniMagick.configure do |config| # don’t need these 3 lines
  config.cli = :graphicsmagick
end

jpg_file = 'blah.jpg'
identify = MiniMagick::Tool::Identify.new
identify << jpg_file
begin
  id = identify.call
  if id.include? "JPEG"
    # do something      
  end
  rescue MiniMagick::Error
    $stderr.printf("MiniMagick::Error file:%s\n", jpg_file)
  end
end   
```  
                                                                                                                                                                          