---
layout: post
title: Domain Driven Design Conclusions
description: What I took from the Domain Driven Design book
date: 23/2/2016
---

I read *Domain Driven Design* by Eric Evans. It was a pretty intense book. By intense, I mean in sheer density of ‘take away’ bolded blocks and diagrams. I’d wager 20% of the page space was diagrams and pictures. Which makes sense, given that the core nuggets of wisdom of the book were in creating a defined map of what the product consists of and is, and all the layers. So the diagrams helped considerably in explaining what he was getting at.

Following in topic and philosophy from other more programming-style/craftsmanship based books, Eric Evans preached communication. For good reason. Bad communication can cause problems at any level of production.

So one way of not falling into that communication trap was of doing this was creating, as the author called it, a ‘Ubiquitous Language’ for the project. Meaning, make a language with words and definitions everyone understands and uses consistently so people are not getting confused or hear one thing and think another. I love this idea. I used to read LessWrong, and one of the points that stuck with me is that there are times when people are not disagreeing with each other on principle, but they are just using different definitions. So the tactic was to look underneath the word and find out what it actually meant in the context. Having a Ubiquitous Language removes the need for it, *if* everyone is using it.

Everything else was really just a means to an end of attaining that robust language and program lay-out. Like how to create models based on the specifications, creating collections of functions, making layers of certain types of logic, dealing with integration and decoupling, and all that.

One of his major examples of doing this was making a program for a shipping company, and he broke it down into the simple models and showed how it evolved to have all these different models, some for things as we understand them, like cargo or a ship, but can also be ‘services’ or things that act on other things. This was especially done in the author’s example of a bank example with accounts and having a calculator-type class.

There was a bounty of other wisdom in *Domain Driven Design*, but those were the points that stuck with me and felt the most applicable, currently with what I am doing and know. The other parts were more involved with bigger projects, which I am not currently experiencing or participating in at the moment. Eventually, maybe, and then I can engage in using the full theory of the book.
