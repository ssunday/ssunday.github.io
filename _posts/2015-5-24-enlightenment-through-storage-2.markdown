---
title: Enlightenment through Storage Part 2
description: Sometimes things are verbose
date: 25/5/2016
---

*You thought I was done, right? Ha. No. This plane doesn't stop. This time relevant programming information is included in today's flight. Free of charge. Probably as useful as a pack of peanuts to someone who is allergic. It's the thought that counts so count this.*

---

**--Beginning Basic Narration of Recording 2--**

"Are you okay?" Anna asks. She is staring at 'Harrison' who is gazing at the computer screen, scowling mildly.

"Yes," he answers, regaining focus in immediate reality.

"Let's continue, alright?"

"Aye--yes. Yes."

"Smooth," Sarela says, "very smooth."

Lapadj does not respond to the invisible Szarehan, instead he turns his attention to the attentive Human and the project at hand--figuring out how to store information in a Postgres database. Thus far, they (Anna) have only created a local Postgres database by the name of `wiki-test`.

"Creating a table," Lapadj says, refocusing the 'conversation,' "that is what we are doing."

"Yeah, as I was saying, the command to create a table is more verbose and we need to think a little before doing it," she explains. "Tables have columns and columns have types. So we have to figure out what we want to store and what type it is."

"We want to store the posts," 'Harrison' says. "That type would be written data."

"Yeah, we probably want the content of the posts to be stored as a text type," Anna says, "because we don't necessarily want to set a specific size for it. But the post can also have other information too. Like the post title."

"That would also be text, no?"

"Sure, or it could be a set amount of chars. Let's go with text because we don't have any set title length and we don't want to truncate someone's title or something."

"Would we also desire a particular way of distinguishing all these 'posts?'" Lapadj asks, almost with an Empirian accent.

Anna's eyes light up at that. "Oh! That makes sense. Like an ID. That'd be a serial type."

"Okay, now that we know all this we can make this table," Lapadj says, "and then put data into it. What is the command to make a table?"

"It'll just be easier if I type it out..."

```
CREATE TABLE posts (id serial, title text, content text);
```

"And that creates the table inside our `wiki-test` database," Anna says as she hits enter and executes the command. "Now posts with those pieces of information can be put into it."

"Praise the Gods," Sarela murmurs. If Lapadj could click in affirmation he would, but all he could do was give a paltry nod to the computer screen.

Before Lapadj could seize control and attempt to do anything constructive with the table, Anna takes the keyboard and mouse and changes from a terminal to a textual editor by the name of 'IntelliJ.'

"We have the base database set up so now we can write some functions in Java to add the posts and so on," she tells him, not even looking at his face.

"Please tell me you didn't neglect to learn some of these 'programming languages,' right, Lapadj?" Sarela questions.

"Ah, yes, *Java*," Lapadj drawls out, ignoring Sarela's mocking words. "To begin we should make an object, something to perform these Postgres-database-related activities." He accentuates his words by gesturing with his hands.

"Yep. `PostgresData` sound good for a name? Not that great, but it is something."

"Nothing is permanent and all things have the capability to change," he says. Sarela snickers.

Anna laughs. "Except for data structures in Clojure." She continues to make little giggling noises until Harrison blinks and she begins to quiet down. "Yeah, you're right. We shouldn't worry too much about names right now--we can always go back and change them. IntelliJ makes it *so* easy with its refactoring abilities."

Not bothering to say anything in response, Lapadj goes ahead and creates a class named `PostgresData` along with a default constructor and a function called `addPost` with parameters for each of the attributes they had specified.

"Nice," is all Anna says as she looks at it. She bobs her head and then takes control to use the editor's function to automatically create tests for the class.

"First test. Something simple-"

"Test?" Lapadj asks.

"Well, yeah, we are going to need to test to make sure the posts actually get added into the Postgres database we made." She pauses and then finishes with: "TDD and all that."

"TDD," he repeats, barely concealing his Empirian accent.

"Test-driven-development," Sarela quickly explains to her companion. "The job description said that. Or did you just brute force your way in. You did. Of course you did. Somewhere, out in this stupid planet, there is a Human that you stole this job from. A Human that knows more than you."

"I thought the concept was idiotic, so I didn't look into it," Lapadj hisses back at her.

"Well, now you are in it," she replies. "I'm just a passive observer; I can't help with idiotic concepts."

The Kharatzara-posing-as-a-Human mutters a curse under his breath. The insult is clearly registered.

Anna continues to stare at him, as she has been since he lapsed into silence from her perspective.

"Are you okay?"

**--Ending Basic Narration of Recording 2--**

---

*To be continued...*
