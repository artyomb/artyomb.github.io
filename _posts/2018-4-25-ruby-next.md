---
layout: post
title:  "Ruby immutable strings"
date:   2018-04-25 11:53:23 +0300
categories: ruby
comments: true
---

All string literals becoming immutable in Ruby 3.  

For now starting with Ruby 2.3, if you add the magic comment   
{% highlight ruby %}
    # frozen_string_literal: true  
{% endhighlight %}
to the file, the string literal for greeting is then automatically frozen 
(meaning it can't be modified). This means that if name is present and we try
to personalize the greeting, a runtime error will be raised.

This includes those created using double quotes (“), single quotes (‘), or the special forms %Q and %q.

## What for?
- **Performance**  
  Since Ruby 2.1, frozen strings have avoided duplicate 
  object allocation by ensuring that identical frozen strings 
  always refer to the same object in memory.  
  
- **Error-prone usage protection**  
  It should protect the code from non-intentional changing of 
  strings constant by design. 

## What if we do need to modify the string?
In case we do need to update the string defined frozen we just have to duplicate it.
{% highlight ruby %}
    new_string = frozen_string.dup.upcase
{% endhighlight %}

    
## Reference links

1. <https://www.pluralsight.com/blog/software-development/ruby-2-3--working-with-immutable-strings->