---
layout: post
title: "Grafista has glyphs with codepoints that are invalid Unicode codepoints e.g. Hex B0001 but which can't be rendered (they render as black boxes) by imagemagick using the pango renderer. Help please!"
---
* Anybody know how to render these non standard custom glyph's like Grafista's `B0001` in a web app or in Python, Rust, Ruby etc. Ideally I'd render the custom glyphs to a PNG so I can make tshirts :-) !
* Source for hex `B0001`  being an invalid Unicode codepoint (<del>I thought it was invalid initially!</del>) is Tim Bray's blog post from [August 14, 2023](https://www.tbray.org/ongoing/When/202x/2023/08/14/Unicode-Scalar-Value) (see also https://www.fileformat.info/info/unicode/char/b0001/index.htm which states:  `U+B0001 is not a valid unicode character.`) : 
```
The text must consist of a sequence of [Unicode scalar values]
(https://www.unicode.org/versions/Unicode10.0.0/ch03.pdf#G7404), 
i.e integers in the inclusive ranges 0-0xD7FF and 0xE000-0x10FFFF.
```
* My toot about this:
    * anybody know anything about custom fonts on Linux (ubuntu 22.04, on dell xps13) or macOS.? My plan was to use the cool graphic glyphs from the [Grafista](https://learn.scannerlicker.net/2016/10/06/making-grafista/) font and make a thunderbird infographic  png out of text in Grafista. unfortunately although the font shows 1600 glyphs i only have access to 360 glyphs and `xfd` on linux shows the wrong glyphs, i.e. not the cool graphic glyphs

### Previously

* July 26, 2023: [April 1 - June 30, 2023 infographic of Thunderbird SUMO Support Questions using the imagemagick 7.x ashlar best fit option](http://rolandtanglao.com/2023/07/26/p2-info-graphic-from-thunderbird-sumo-questions-april-june-2023/)        



