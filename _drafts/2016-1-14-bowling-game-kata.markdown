---
title:  "Bowling Game Kata"
description: A first step into TDD through the bowling game kata
#date: 13/1/2016
---
The topic for this part of my coding journey as a software apprentice is test driven development (TDD). The language of choice for this endeavor is Ruby with Rspec.

To start off this segment, I learned about ‘katas,’ little burst of TDD programming that are meant to be done repeatedly and consistently to engrain the ideals and rhythm of test driven development into your mind and being. Katas are Japanese term for a training exercise to hone one’s skills that were appropriated into programming lingo by Dave Thomas (according to Wikipedia, anyway.)

The first Kata I did was a bowling game kata, hence the title of this diary-blog-post-thing. In the bowling game, one can roll and one can take score of a total game. There can be spares and strikes. Learning the rules of bowling was a one of the more annoyingly challenging aspects of it. My knowledge of bowling extends primarily to Wii-fit bowling and being able to always roll the ball into the gutter. I persevered though, through sheer force of muddling.

With TDD, one writes the tests for the class or program first. You outline the expectations first and then write the actual code to fulfill those requirements. 

So, the first test written for the bowling game kata is when the player scores all 0s for all rolls, making a grand total of 0 for the entire game. 

Then we run rspec to test it out and look it fails miserably. Why? Well, we don’t have a bowling game kata class or any methods. That might be why.

So then we add them, just the little bit needed to make the test pass. The easiest way to do this is add a scoring and rolling method, and having the former only return 0. With that, it passes.

```ruby
def score
  0
end
```

Then when that is done we add more tests, not ones we know will succeed, but ones we know will fail as we have not added the actual functionality to the bowling game class. In this case it was adding the test case for a game of all 1s, which would add up to 20. This, of course, does not work in the current state of the BowlingGameKata class, as there really isn't a roll or score method that does anything constructive. 
