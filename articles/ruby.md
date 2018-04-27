---
layout: page
title:  "Ruby language"
categories: ruby
comments: true
order: 110
---
Looking for Ruby language online test? Me too!

## Testdome.com
Pure Ruby language test. There are only three Live Coding Questions. 
1. Palindrome - A palindrome is a word that reads the same...
2. File Owners - Implement a group_by_owners function...
3. Path - Write a function that provides change...
<https://www.testdome.com/tests/ruby-online-test/52>  
### Answers:
{% highlight ruby %}
    # Palindrome
    word.downcase == word.downcase.reverse 

    # File Owners
    files.reduce({}) do |r, pair|
      (r[pair[1]] ||= []) << pair[0]
      r
    end
    
    # Path
    @current_path += "/#{new_path}"
    @current_path.gsub!(/\/[^\/]+\/\.\./, '') while @current_path =~ /\.\./
{% endhighlight %}


I like there is online code editor and test. 
You have to write the code that passes the series of unit test to complete the task.
Sadly there arn't more test.

## CodeQuizzes.com
Very good list of test with descriptive answers. 
The test cover a lot of Ruby aspects from Beginner through Advanced level.

<http://www.codequizzes.com/ruby>

It is the best way to make you Ruby knowledge coverage test for now.

## More ...
Please leave a comment with the good online tests you know.