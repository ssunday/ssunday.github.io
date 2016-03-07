---
title: Roman Numerals Kata
description: Converting Arabic to Roman numbers in Ruby as a Kata
date: 1/2/2016
---

The Roman Numerals Kata is pretty straight forward. Take an arabic number and convert it into a roman numeral. 4 becomes IV and so on. This is a common programming problem that I have done probably three times already, each in a different language. Python, Java, and C++. And now for this fourth time, in Ruby, I used the power of TDD to guide me.

The initial case is pretty simple. 1 becomes I.

```ruby
it "returns I for 1" do
    expect(@roman_numerals_kata.get_roman_numerals(1)).to eq "I"
end
```

And the easiest way to make this test pass is to return I. But that stops working with 2. The next iteration has the get_roman_numerals function looking something like this:

```ruby
def get_roman_numerals(number_to_convert)
      “I”*number_to_convert
end
```

Which takes the number to convert and multiplies it by I, so 2 would give II and 3 would give III, but 4 would return IIII, which is not correct. It should be IV.

This is where I made the leap. I recalled in Java that I used a hash to store the different roman numerals and their arabic counterparts, so I used the same principle with this Kata.

In the RomanNumeralsKata class I created this constant:

```ruby
NUMERALS = {1000 => "M", 500 => "D" , 100 => "C", 50 => "L", 10 => "X", 9 => "IX", 5 =>  "V" , 4 => "IV", 1 => "I"}
```
Which has key value pairs of the arabic numbers and their roman equivalents. Specifically, the major ones and the 'unique' ones. After creating this, it was as simple as iterating through it and doing the same subtracting/concatenation process like with the [coin changer.] (http://ssunday.github.io/2016/coin-change-kata/)

Final function:

```ruby
  def get_roman_numerals(number_to_convert)
    roman_string = ""
    NUMERALS.each do |number, roman_number|
      while number_to_convert >= number
        roman_string += roman_number
        number_to_convert -= number
      end
    end
    roman_string
  end
```

With this, the code passes a variety of test cases such as these:

```ruby
it "returns XIX for 19" do
    expect(@roman_numerals_kata.get_roman_numerals(19)).to eq "XIX"
  end

  it "returns DLXXIV for 574" do
    expect(@roman_numerals_kata.get_roman_numerals(574)).to eq "DLXXIV"
  end

  it "returns MCCXIX for 1219" do
    expect(@roman_numerals_kata.get_roman_numerals(1219)).to eq "MCCXIX"
  end
```

And there it is. It was very short for me since I was already pretty familiar with the problem. Adding test cases was probably the most difficult part. I consulted an online converter and put in some numbers that would be ‘troublesome.’ In total I have 9 (or IX) test cases, I could add more, but as the first edition of the kata I am content with leaving it the way it is until I do it over again and make improvements.

[All the code on Github.](https://github.com/ssunday/RomanNumeralsKata)
