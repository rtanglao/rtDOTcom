---
layout: post
title: Yosemite RMagick magic 
---
If you cannot install RMagick using brew on Yosemite 10.10.2, then for the 3 of you who care, here's how to do that (copied and pasted from: [Stack Overflow](http://stackoverflow.com/questions/28247947/fail-to-install-rmagick-on-mac-10-9-5)):

    $ git clone -b RMagick_2-13-4 git://github.com/gemhome/rmagick.git
    
    Merged the fix code (replace related code in ext/RMagick/rmmain.c) .
    #if defined(HAVE_GETMAGICKFEATURES)
    // 6.5.7 - latest (7.0.0)
        features = rb_str_new2(GetMagickFeatures());
    #elif defined(MagickFeatures)
    // 6.5.7 - latest (7.0.0)
        features = rb_str_new2(MagickFeatures);
    #elif defined(MagickSupport)
    // 6.5.5 - 6.5.6
      features = rb_str_new2(MagickSupport);
    #else
        features = rb_str_new("unknown",7);
    #endif

    And then installed it.

    $ cd rmagick/
    $ gem build rmagick.gemspec
    $ gem install --local rmagick-2.13.4.gem
    Building native extensions.  This could take a while...
    Successfully installed rmagick-2.13.4
    1 gem installed

