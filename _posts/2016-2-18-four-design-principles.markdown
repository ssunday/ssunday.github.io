---
layout: post
title: Four Rules of Simple Design
description: Some thoughts on code design principles detailed by Corey Haines
date: 18/2/2016
---

I just finished reading *Understanding the Four Rules of Simple Design* by Corey Haines. It was only like 90 pages, so I knocked it out in less than a day. It was an easy read asides from the length, and it was to the point with what it was talking about, which I appreciated. Also helped that I had done the Game of Life before and have been programming in Ruby, so the code and context was familiar.

The four rules of good code design the author expounded upon are:

 1. Tests pass
 2. Express Intent
 3. No duplication/do not repeat yourself
 4. Simple


The first one is pretty obvious. Another way that I think of it is that that code works as specified. Considering tests are written to makes sure the code works as intended, it really is just another way of saying the code is functional. Which should be a priority, regardless of how you design anything.

Rule number two is a bit more stylistically driven. A tip for style within the design of the program. Corey Haines explained and demonstrated it through making coherent function and variable names. Expressing the intent for the code through naming and organization. The reason for the codes existence should be clearly explained so if a person reads it they can understand what is going on without having to stress themselves too much.

The no duplication/do not repeat yourself is a way to minimize code repetition and to streamline design. This can be through creating functions and methods, or by using inheritance. In one of Haines’s examples, he removed duplication in a Cell class by having the two cells inherit from another class that contained the duplicated attributes and methods. This is by far the most straight forward rule. I like applying it, because if you use it can make the code much cleaner and problems much simpler.

The last one is perhaps the most abstract. Simple. What does Haines mean by simple? Basically not making it overtly complicated. Don’t extract too far. Make the class distinctions sensible and not overtly convoluted. Don’t have code that doesn’t do anything. Make it minimalist in structure and presentation. Simple.

I basically agree with all these rules—they are not rules that are too specific or potentially too niche. They are principles that good code, regardless of context, can typically adhere to. Universal standards. Guidelines may be a better word, but it doesn’t particularly matter. These rules are good things to do as they make code more functional and more easily maintainable. Which are both excellent things for code to be.
