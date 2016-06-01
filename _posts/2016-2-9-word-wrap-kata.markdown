---
layout: post
title: Wrapping My Mind Around the Word Wrap Kata
description: Formatting strings and surprise recursion
date: 9/2/2016
categories: kata
---

The gist of the Word Wrap Kata is to create a function that takes in a string and a length of a ‘column’ and returns a formatted string with new lines placed such that that maximum length is not exceeded by the string.

So if given ‘hello’ and 3, it would return:

hel
lo

In Ruby-String lingo this is “hel\nlo”.

The function makes it so newlines are inserted so that the string is cut off where it needs to so the string does not pass by the defined column length.

To start this off, I began with the simplest test case. When the string is already less than the maximum length and nothing needs to be changed.

```ruby
it "does not alter a string of less than max length" do
    max_length = 10
    string = "hello"
    expect(@word_wrap_kata.wrap(string, max_length)).to eq string
  end
```

And, of course, the easiest way to get this accomplished is to return the string passed in.

```ruby
def wrap(string, max_length)
    string
end
```

For the next step, with a case where the string does split, the answer is a bit more complicated.

How I did this was I created an if else block where if the string was less than the maximum length I would simply return it, and in the else block I would split the string apart, having one piece of the string to the max length followed by a “\n” and then concluding with the rest of the string. This works only when the string is broken up into two pieces. For any more, the function will fail to meet the tests, such as this one:

```ruby
it "breaks a string into three parts" do
    max_length = 2
    string = "hello"
    expect(@word_wrap_kata.wrap(string, max_length)).to eq "he\nll\no"
  end
```

Getting it to work with all cases is a bit trickier. I broke down and perused the internet for help. What I learned was that the consistent way of doing this involved recursion. I left the if block the same, but in the else block I’d take the string to the max length passed in, add a new line, then call the wrap function with the rest of the string and the same column length.

With this added recursion, the test cases pass, except for ones where the string breaks such that there would be a new line at the end of the string which is not something we want or need. To fix this, I just added a .rstrip at the end of the wrap function call, stripping any returns on the right side.

Then it all works.

Final Wrap function:

```ruby
def wrap(string, max_length)
    if string.length < max_length
      return string
    else
      return string[0, max_length] + "\n" + wrap(string[max_length..-1], max_length).rstrip
    end
  end
```

[For the complete code, check out the repo on Github.](https://github.com/ssunday/WordWrapKata)
