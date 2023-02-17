---
layout: post
title: "How To label an image with an emoji using ruby rmagick with imagemagick? A: Use XML escape e.g. &x1234;"
---
* For my 3 followers :-) who want to create images with  emojis with ruby :-). 
* Sadly copying and pasting the emoji doesn't work.
* Neither does specifying the `Noto Color Emoji` font (imagemagick fails with "cannot read font").
* But oddly, copying and pasting an emoji into the command line e.g. `magick` or `convert` work with copy/pasted emojis.
* Finally, I could not get the `rmagick/imagemagick` combo to work without using [pango](https://www.imagemagick.org/Usage/text/#pango) which uses XML escapes for unicode characters like emojis.

### Code 
```ruby
# convert pango:'a🤳Hello! 😀How are you?' example.png # Selfie emoji is 1F933
require 'rmagick'
image = Magick::Image.read('pango:&#x1F933;The <b>bold</b> and <i>beautiful</i>').first
image.write('pango.png')
```

<https://gist.github.com/rtanglao/0d0e9c5a9dbd7ffae7825acd5544140c>

### Previously
* March 2, 2019: [It's March 2, 2019: has the current podcast boom busted yet?](http://rolandtanglao.com/2019/03/02/p1-is-the-current-podcast-boom-over-yet/)