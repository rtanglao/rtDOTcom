---
layout: post
title: "RMagick doesn't support smush to align horizontal images at the bottom but MiniMagick does; you need gravity set to `south` to anchor images to the bottom ie. `south`"
---
* From [Mastodon](https://elk.zone/devdilettante.com/@roland/111067680184544895): Today I Learned, RMagick doesn't support `smush` ([imagemagick docs for smush](https://imagemagick.org/script/command-line-options.php#smush),[ RMagick docs for montage don't mention smush](https://www.rubydoc.info/gems/rmagick/Magick/ImageList/Montage)) to align horizontal images at the bottom but [MiniMagick](https://github.com/minimagick/minimagick) does! Stack Overflow:[imagemagick montage - how to align images to bottom](https://stackoverflow.com/questions/60357036/imagemagick-montage-how-to-align-images-to-bottom)
* The othe important thing to note is you need to set `gravity` to `south` to anchor the images at the bottom instead of at the top.

### Code
From: [create-emoji-question-graphics.rb](https://github.com/rtanglao/rt-tb-noto-emoji-2023/blob/main/create-emoji-question-graphics.rb)

```ruby
require 'mini_magick'
def montage_images_horizontally(image_to_be_appended, image)
  MiniMagick::Tool::Magick.new do |m|
    m.gravity('south')
    m << image
    m << image_to_be_appended
    m.smush.+(10)
    m << image
  end
end
```

### Previously

* February 17, 2023: [How To label an image with an emoji using ruby rmagick with imagemagick? A: Use an XML entity escape e.g. &x1234; with the pango text renderer](http://rolandtanglao.com/2023/02/17/p1-howto-label-image-emoji-imagemagick-rmagick/)

