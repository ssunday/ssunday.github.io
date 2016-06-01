---
layout: post
title: Coin Change Kata
description: Another week, another kata. This time with money.
date: 25/1/2016
---

It feels like the more TDD katas I do, the easier they get. The Prime Factors Kata was only difficult the first time around. Subsequent go-throughs were quite simple and I barely made any major mistakes. The Bowling Game was a steeper curve because it was my first.

Now the Coin Change Kata, my third, went very easily. The function being performed by the Coin Change class is to take an amount and return the smallest number of coins that make up that amount. Like for six cents it would return a nickel and a penny, not six pennies.

Which seems simple enough, and it kind of was.

The basic test case I started with was:

```ruby

it "returns a penny for a penny" do
    expect(@coin_change.change(1)).to eq [1]
  end

```

And then I proceeded to make a function to merely return [1]. Test passed! Then I added the case of two pennies, and then it all fell apart, to be expected.

The second iteration of the change function involved creating a while loop based on the condition where the amount was greater than zero and every time subtracting 1 from the amount passed in adding 1 to the list and then finally returning the list. With this change, it works and the test passes.

But with the case of passing in six cents and expecting a nickel and a penny, it, again, falls apart, because it is only dealing with pennies in its mind and design. This is where I leaped into making it work for all cases, rather easily.

I began with thinking about the different coin values, 25, 10, 5, and 1, and creating a list of those values in that order. Then I iterated over those values and while the amount was greater than it, subtracted the coin value and added the value to the list. The for loop handled moving through the list, so there was no need to do anything else. Just return it and it was done.

The final function looks like this:

```ruby
def change(amount_of_money)
    change_amounts = [25,10,5,1]
    change = []
    change_amounts.each do |coin|
      while amount_of_money >= coin
        change << coin
        amount_of_money -= coin
      end
    end
    change
  end
```
[And the complete code is on github.](https://github.com/ssunday/CoinChangeKata)

The solution to the problem felt a bit more intuitive than the other katas, which may also explain why it was easier for me. Or I’m just getting quicker with doing TDD and making the steps. Either way, it is done.
