---
layout: post
title:  "Stargate the ancients' language"
categories: ruby
comments: true
---

I'm a big fan of the Stargate series! I was thinking about the unordinary symbols of the ancients' language.

I found their form to have a bit-like structure. So I started with a randomly generated pattern NxN.

![glyph](https://raw.githubusercontent.com/artyomb/ruby_gl/master/glyph_0.jpg){:style="width:100px; display:block"}

Then I found some patterns don't look _good_. So, I added check functions to exclude these patterns.

- no_quads? Exclude 'bold' structures.

- no_chess? Exclude 'chess' structures.

[https://github.com/artyomb/ruby_gl/blob/master/**glyphs.md**](https://github.com/artyomb/ruby_gl/blob/master/glyphs.md)

The script generates new glyphs on each key press. Press 's' to take the screenshot.

An extended alphabet of the ancients' language!