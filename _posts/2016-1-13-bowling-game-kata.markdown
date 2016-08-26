---
layout: post
title:  "Bowling into TDD"
description: My first step into TDD through the bowling game kata
date: 13/1/2016
category: kata
---
The central topic for this part of my coding journey as a software apprentice is test driven development (TDD), which I am very unfamiliar with. The language of choice for this endeavor is Ruby with rspec, which I am also unfamiliar with.

To start off this segment, I learned about ‘katas,’ little burst of programming that are meant to be done repeatedly and consistently to engrain the ideals and rhythm of test driven development into your mind and being. Katas are a Japanese term for a training exercise to hone one’s skills that were appropriated into programming lingo by Dave Thomas [(according to Wikipedia, anyway.)](https://en.wikipedia.org/wiki/Kata_(programming))

The first kata I did was a bowling game kata, hence the title of this diary-blog-post-thing. In this simplistic bowling game, one can roll and one can take score of a total game. There can be spares and strikes. Learning the rules of bowling was a one of the more annoyingly challenging aspects of it. My knowledge of bowling extends primarily to Wii-fit bowling and being able to always roll the ball into the gutter. I persevered though, through sheer force of muddling and the wikipedia page for the rules of the game.

With TDD, one writes the tests for the class or program first. You outline the expectations first and then write the actual code to fulfill those requirements. Which actually makes sense in a lot of ways, contrary to how programming is generally taught. I like the idea, but learning how to execute is a bit of a curve (bowling) ball.

Starting off at the base case is the usual way of going about TDD, and in this situation that would be when the player scores 0 total, in other words they failed to hit any pins. So, the first test written for the bowling game kata is when the player scores all 0s for all rolls, making a grand total of 0 for the entire game. 

In Ruby and rspec, the test looks something to the effect of this:

```ruby
it "in a game of all 0s the score is 0" do
  20.times do
    @bowling_game_kata.roll(0)
  end
  expect(@bowling_game_kata.score).to eq 0
end
```

I ran rspec to test it out and it fails miserably. Why? Well, there isn't a bowling game kata class or any methods. That might be why.

To remedy this, I added just the little bit needed to make the test pass. The easiest way to do this is add a scoring and rolling method, and having the former only return 0. With that, it passes.

```ruby
def score
  0
end
```

Then, following TDD-style philosophy, when that is done we add more tests, not ones we know will succeed, but ones we know will fail as we have not added the actual functionality to the bowling game class. In this case it was adding the test case for a game of all 1s, which would add up to 20. This, of course, does not work in the current state of the BowlingGameKata class, as there really isn't a roll or score method that does anything constructive.

The next step is to add those functions and to make them work to make the tests passed. How I did this was I created an array of the bowling ball roll score values, like how many pins were knocked down and when the .roll() function is called the score is appended to it. The scoring function was then modified to sum the contents of the array.

With those additions, the test passes.

But bowling isn't just that simple. There are spares and strikes to deal with. They have their own respective tests and  methods that need to be implemented. Because the code wasn't written knowing about those cases, it has to be restructured and altered to make it all work.

After all these changes to increase functionality and make the tests pass, the scoring function looks like this:

```ruby
def score
  roll_index = 0
  total_score = 0
  frame_count = 0
  while frame_count < 10
    if spare?(roll_index)
      total_score += 10
      total_score += spare_bonus(roll_index)
      roll_index += 2
    elsif strike?(roll_index)
      total_score += 10
      total_score += strike_bonus(roll_index)
      roll_index += 1
    else
      total_score += sum_of_frame(roll_index)
      roll_index += 1
    end
    frame_count += 1
  end
  total_score
end
```

[The completed code is here on Github.](https://github.com/ssunday/BowlingGameKata) There were a bunch of other changes that were made to make the code easier to read, fall more in line with Ruby style, and improve the description of the test cases.

The Bowling Game Kata was my first real go-at TDD and I learned a ton about it and Ruby. I'm getting into the TDD style of programming, and I think it is growing on me. Slowly but surely.
