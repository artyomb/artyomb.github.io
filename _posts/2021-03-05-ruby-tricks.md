---
layout: post
title:  "Ruby tricks"
categories: ruby
comments: true
---

Let's start with some return object modification: 

<iframe src='https://tech.io/snippet-widget/VgamWZK' width='100%' frameborder='0' scrolling='no' allowtransparency='true' style='visibility:hidden'></iframe>

<!--
```ruby
def not_so_simple(str)
  str.define_singleton_method :special? do 'yes!' end
  str
end
str = not_so_simple('Hello')
puts str.special? # yes!
```
-->

# What's going on?
How can we find out the way the object in ued?


<iframe src='https://tech.io/snippet-widget/6dcJGlv' width='100%' frameborder='0' scrolling='no' allowtransparency='true' style='visibility:hidden'></iframe>

<!---
```ruby
class InspectUsage
    def initialize(obj)
        @object = obj
    end
    
    def method_missing(name, *args, &block)
        puts "Call method(#{@object}): #{name} (#{args} #{block})"
        @object.send name, *args, &block
    end
end

str = InspectUsage.new "Hello"
puts str.size

array = InspectUsage.new [1,2,3]
puts array.reduce &:+

proc = InspectUsage.new( proc { puts 'hello' })
puts str.gsub /.*/, &proc
```
-->

<script src="https://files.codingame.com/codingame/iframe-v-1-4.js"></script>
<script>
    document.querySelector("iframe").addEventListener( "load", function(e) {
        this.contentWindow.postMessage("sendSize", '*');
    });
</script>
