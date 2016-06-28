---
layout: post
title:  "Another Kata: Prime Factors"
description: Making a prime factors calculator using TDD
date: 19/1/2016
categories: kata
---

Having drained the Bowling Game Kata of all its life by practicing it constantly as I ought to be, I have moved onto another kata. The kata that I have chosen is the Prime Factors Kata, which performs the calculation of finding the prime factors for a given number.

The simplest case for this is when the input is 2 and the return is 2:

```ruby
it "should return 2 for an input of 2" do
    prime = @prime_factors_kata.calculate(2)
    expect(prime).to eq 2
end
```
And the easiest way to do this is just to make calculate return 2. But this approach fails, of course, when another case, say for 3, is added. Then changing it to return the given number makes both cases work.

```ruby
def calculate(number)
    number
end
```

Throwing a wrench into this is putting in a number that doesn’t return just a single factor, but a multiple of factors. Like 8, for instance. The calculate function should return [2,2,2], signifying that those are the prime factors of 8.

But at the moment calculate only returns a single number, so I needed to refactor the code and tests to return a list of numbers rather than individual numbers. This was simple enough but getting the expected output of [2,2,2] required adding more logic. In this case it was constructing two while loops, with the condition being that the number’s mod of 2 and 3 was zero, and appending those to the list of factors. The number would be redefined by the division of the respective number and the loop would continue until it could no longer be evenly divisible by 2 and 3. Returning the factors list makes the test pass.

Code that does this:

```ruby
def calculate(number)
    prime_factors = []
    while number % 2 == 0
      prime_factors << 2
      number /= 2
    end
    while number % 3 == 0
      prime_factors << 3
      number /= 3
    end
    prime_factors
end
```

This only works for 2 and 3. What if the number is 14 and has prime factors of 2 and 7? Currently the calculate function would only return [2], not [2,7].

![Failed Test](/assets/post-images/PrimeFactorsKataError1.png)

This is where the serious refactoring begins. I looked up ways to go about making a prime factors algorithm, and a common way to do this is to use the [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes), which basically is an algorithm designed to find prime numbers up to a given number. I’m not that savvy with mathematical algorithms, so I used [Rosetta Code](http://rosettacode.org/wiki/Sieve_of_Eratosthenes#Ruby) to get the ruby code for it. I did some minor modifications to it so it returns an enumerator so the calculate function has a more streamlined way of working.

The Eratosthenes function:

```ruby
def eratosthenes(number)
  candidates = [nil, nil, *2..number]
  (2..Math.sqrt(number)).each do |i|
    (i**2..number).step(i){|m| candidates[m] = nil} if candidates[i]
  end
  candidates.compact.to_enum
end
```

Then I refactored the calculate function to use the list of prime numbers up to the given number to go through and get the prime factors. It uses mod in the same way as before, but instead of the number being divided by 2 or 3, it is being divided by whatever current prime we are on in the prime candidates given to us from the Sieve of Eratosthenes function. Using .next of the enumerator class, the function goes through that list.

The final code for calculate:

``` ruby
def calculate(number)
  prime_factors = []
  prime_candidates = eratosthenes(number)
  current_prime = prime_candidates.next
  until Prime.prime?(number)
    if number % current_prime == 0
      prime_factors << current_prime
      number /= current_prime
    else
      current_prime = prime_candidates.next
    end
  end
  prime_factors << number
  prime_factors
end
```

And it works for the multitude of cases supplied.

This kata had, I think, a smaller amount of larger steps than the [bowling game kata](http://ssunday.github.io/2016/bowling-game-kata/). Adding the functionality to make it work for more than 2 or 3 required using another algorithm and refactoring around it, but after that was done it was basically all finished. I liked this kata more because of that. It got to the point faster.

[Here is the completed code on github.](https://github.com/ssunday/Prime-Factors-Kata)
