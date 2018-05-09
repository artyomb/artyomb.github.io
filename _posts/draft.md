# array#to_proc
<https://thepugautomatic.com/2014/11/array-to-proc-for-hash-access/>


# To add class functionality it is better to place your extensions 
to a module and prepend it instead of doing a direct patch in class namespace.
 
# Also Hash.to_proc 
```ruby
h = {
  'a' => '1',
  'e' => '2',
  'i' => '3',
  'o' => '4',
  'u' => '5'
}
h.default = ''
"hello world".gsub /[aeiou]/, h
# => "h2ll4 w4rld"
```
Any matches you have in the hash, no matter the length, will check the hash for a key and get the value.
If the hash has a default return value set as well then every missed key will substitute a default result into the string.


# feature Hash#to_proc, Hash#default 
```ruby
h = { a: 1, b: 2, c: 3, d: 4 }
h.default = ''
[ :a, :c, :d, :b ].map(&h)
# => [ 1, 3, 4, 2 ]
```
And your hash can have a default value or proc set for non entry values. So much win!

 