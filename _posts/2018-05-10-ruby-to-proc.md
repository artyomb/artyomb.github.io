---
layout: post
title:  "Ruby .to_proc"
date:   2018-05-10 11:53:23 +0300
categories: ruby
comments: true
---

Beware not to forget about **.to_proc** conversions.

Since Ruby 2.3.0 **Hash** class has a **.to_proc** conversion. It's pretty useful with `&` operator. 
```ruby
h = { a: 1, b: 2, c: 3 }
[ :a, :b, :c, ].map(&h) # => [ 1, 2, 3 ]
```
Another case is using Hash with  **gsub** 
```ruby
h = {  'a' => '1',  'b' => '2', 'c' => '3' }
"xxxabcxxx".gsub /[abc]/, h # => "xxx123xxx"
```
## default
And very useful is Hash **default** for non entry values.
```ruby
h = {  'a' => '1',  'b' => '2', 'c' => '3' }
h.default = 'Y'
"xxxabcxxx".gsub /[abcx]/, h # => "YYY123YYY"
```
You may use default_proc to create new key-value pairs.
```ruby
h = {  'a' => '1',  'b' => '2', 'c' => '3' }
h.default_proc = proc { |h, c|  h[c] = c.upcase }
"xxxabcxxx".gsub /[abcx]/, h # => "XXX123XXX"
```
Interesting that we can do cache strategy as simple as follows
```ruby
cache = Hash.new { |cache,url| cache[url] = open(url) }
puts cache['http://site.com/resource']  
```

## Array#to_proc
I have found interesting suggestion to add **to_proc** to array with similar functionality. 
<https://thepugautomatic.com/2014/11/array-to-proc-for-hash-access/>

If that fits your eyes
```ruby
[ { name: "A" }, { name: "B" } ].map(&[:name])  # => [ "A", "B" ]
```
Here the way you can get it
```ruby
class Array
  def to_proc
    ->(h) { length == 1 ? h[first] : h.values_at(*self) }
  end
end
```
And that will work with multiple keys too
```ruby
[ { name: 'A', 'age' => 41 }, { name: 'B', 'age' => 42 } ].map(&[:name, 'age'])
# => [ [ "A", 41 ], [ "B", 42 ] ]
```