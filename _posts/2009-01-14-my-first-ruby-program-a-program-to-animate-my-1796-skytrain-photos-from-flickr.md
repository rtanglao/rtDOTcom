---
layout: post
title: My first ruby program - a program to animate my 1796 Skytrain Photos from flickr
created: 1231992079
---
<p>
Let's say you had 1796 photos in a directory from flickr and wanted to animate them in <a href="http://shoooes.net/">Shoes</a> which is built on <a href="http://www.ruby-lang.org/en/">Ruby</a>, how would you do it?
</p>
<p>
Here's how I did it (forgive my bad code, it was just a fun 1st project and of course you could do this in QuickTime Pro with no programming but that wouldn't be as much &quot;fun&quot; :-) !):
</p>
<textarea id="code" class="codeedit" name="code2" cols="80" rows="12">Shoes.app {
  flow :width =&gt; 1024, :height =&gt; 768, :margin =&gt; 50 do

Dir.chdir(&quot;/a directory with 1796 skyte photos&quot;)
skyte_pics = Dir.glob(&quot;*.jpg&quot;)
size = skyte_pics.size
@skyte =       image skyte_pics[0]
        animate(200)  do |frame|
          close if frame &gt; size
          @skyte.path = skyte_pics[frame]
        end
  end
}</textarea>
