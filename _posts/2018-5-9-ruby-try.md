---
layout: post
title:  "Ruby try &."
date:   2018-05-9 11:53:23 +0300
categories: ruby
comments: true
---

Safe navigation operator

Ruby 2.3.0 introduces new operator `&.` which acts like object#try from ActiveSupport.
```ruby
person = Person.new
puts "Money: #{person&.account&.money}"
```
# Not so simple
You may guest that `foo&.bar` is equivalent to `(foo == nil) ? nil : foo.bar`. But it's not.
```ruby
def foo 
  obj = nil
  (obj == nil) ? nil : obj.attr
end

foo += 1 # undefined method `+' for nil:NilClass
```
While using operator `&.` you are safe.
```ruby
obj = nil
obj&.attr += 1 # nil
``` 
The operator `&.` checks for **nil** value and gracefully interrupts whole expression and return **nil**. 

 

# Using with Hashes
The same semantics for Hashes may look like this
```ruby
h = {key1: 1, key2: { subkey: 's'} }

p h[:key3]&.[](:subkey)
```

But it's better to use `dig` method since ruby 2.3
```ruby
p h.dig  :key3, :subkey
p h&.dig  :key3, :subkey # even that safe
```
# Attention
Some cases may lead to misunderstanding.
- The `&.` syntax only skips **nil** but recognizes **false**.
  It is not exactly equivalent to the `s1 && s1.s2 && s1.s2.s3` syntax.
  The right interpretation is 
  ```ruby
  foo&.bar
  (foo == nil) ? nil : foo.bar # almost the same, see above
  ```

- You should avoid using `nil?` check with `&.` operator. 
  It handles **nil** already and you may get unexpected result
  ```ruby
  nil&.nil? # => nil
  nil.nil? # => true
  ```
- The undefined variables are still undefined
  ```ruby
  obj&.attr # undefined local variable or method `obj' for main:Object
  obj = 1
  obj&.attr # undefined method `attr' for 1:Integer 
  ``` 
- Don't do assignment to `&.` operator result
  ```ruby
  obj&.attr += 1 
  ```


