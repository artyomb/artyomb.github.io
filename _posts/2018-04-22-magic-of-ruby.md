---
layout: post
title:  "Magic of Ruby &"
date:   2018-04-22 11:53:23 +0300
categories: ruby
comments: true
---

Let's start from the basics. Ruby has the following syntax feature: 
{% highlight ruby %}
collection.map(&:name)
{% endhighlight %}

which means

{% highlight ruby %}
collection.map{ |el| el.name }
{% endhighlight %}

It works because Ruby expands `&:name` to `&:name.to_proc` and adds method **to_proc** for the Symbol class

{% highlight ruby %}
class Symbol
  def to_proc
    Proc.new do |obj, *args|
      obj.send self, *args
    end
  end
end
{% endhighlight %}

### Consequences
The `&` operator may take any **proc** object or the objects that can be converted to proc by **to_proc** method.

{% highlight ruby %}
inc = proc { |e|  e + 1 }
collection.map(&inc)
{% endhighlight %}

You can use the self's methods 
{% highlight ruby %}
collection.map(&method(:foo))
# ==
collection.map{ |el| foo(el) }
{% endhighlight %}

### Parameters
You can supply arguments to `&` syntax too. (ref [2]) 

{% highlight ruby %}
class Symbol
  def with(*args, &block)
    ->(caller, *rest) { caller.send(self, *rest, *args, &block) }
  end
  alias call with
end

a = [1,3,5,7,9]
a.map(&:+.with(2))
# or
a.map(&:+.(2))
# [3, 5, 7, 9, 11]
{% endhighlight %}

As we saw above the `proc` object could be taken from the method of an instance so for the simple arithmetic this works too.
{% highlight ruby %}
a = [1,3,5,7,9]
a.map(&2.method(:+))
# [3, 5, 7, 9, 11]
a.map(&2.method(:*))
# [2, 6, 10, 14, 18]
{% endhighlight %}


### Reference links
Compiled from the following posts

1. <https://stackoverflow.com/questions/1217088/what-does-mapname-mean-in-ruby>
1. <https://stackoverflow.com/questions/23695653/can-you-supply-arguments-to-the-mapmethod-syntax-in-ruby>