---
layout: post
title: Surviving the Plan - 3
description: Plans are for the foolishly brave
date: 5/8/2016
category: recordings
---

*So I've been actually writing lately instead of editing and I keep accidentally switching to present tense with dialogue. I blame this blog. GG.*

---

**--Beginning Expressive Narration of Recording 29--**

"What are we working on now?" Lapadj asks as he and Anna greet the first moments of Recording 29 by taking their normal positions at their usual desks.

"A repository function to search through the database for posts," Anna replies. "That is next on the stack."

"Do we not already have that? Searching by key?" Lapadj inquires.

Hope for less work is clearly on his countenance, along with anxiety to finish the day and meet Mark, as we all most certainly are. I will endeavor to make this brief and as descriptive as possible to get to the more entertaining Recordings.

"No," she answers. "This is going to be a search on title."

His eyes go blank.

Grapefruit vibrates in his coat, which forces him to take her out and place her to the side. "This is more exciting. When you figure it out, it will make you feel like you actually accomplished something."

"That really does not mean anything to him, Grapefruit," Sarela says.

"How wonderful," Lapadj dryly says to both of them.

"It really is," Anna says with a grin. "It'll make it so people can search for posts in a search bar. But we are just doing the back end for it. The front end is-"

"Someone else's work," Lapadj finishes.

"Exactly, Harrison. So let's get to it, eh?"

"Yes."

"It seems you used up all your acting reservoirs during lunch with Mark," Sarela remarks. "This should be good."

"Seeing Mark and Lapadj meet up later should definitely be exciting," Grapefruit chimes.

"It should be. But it is not happening. Not yet. He needs to do what he came here for. Programming."

He had been doing that while Sarela and the Goddess talked for a short while. His hands touch the keys of the keyboard firmly as he and Anna set up the test and function for the full text search they will make. The Clojure files are the same as with the repository. The function is joining among them.

"So I simple search by title?" Lapadj inquires. He begins to set up a Korma `exec-raw` statement. "Exact match?"

"No, we want to use 'like,'" Anna answers. "So we can search for titles that somewhat match the input. People aren't always correct or know exactly what they are searching for so we have to help them out a bit."

This concept forces Lapadj to re-evaluate his privilege in being an Empirian. He blinks and goes to silence. Anna takes over and starts typing to illuminate the concept.

"Etae to, Spine, etae to," he whispers to my ever-present presence. "What would we exist if not for you?"

"There is a high chance that the Empire would fall apart. Such a high chance that it would not come to pass," I reply to him.

He bristles. "Should I feel special for conversing with you directly?"

"No. I am holding over one hundred billion partially deep conversations at this moment."

"Well, thank you for giving me some of your limitless attention."

To that, I do not reply. Sarela laughs and he returns to working with Anna. She has typed only a few lines of code, but the framework of what it is is now present before them on the screen.

"So for our function we are going to pass it a title," Anna says. "So in the test we are going to save a few entries and we'll have our test input match one of them."

"Logical," he says. The test has been constructed for their usage.

"Yeah." The test fails in a show of red as she hits save. "So now to the function."

"Yes," he mutters. "How do we use like?"

He experiments with the query:

```sql
SELECT * from posts where title like ?
```

"That's a good start," she says. "You have the right idea."

But, when he saves the file, the test fails.

"How can that be a right idea when it does not work?" Lapadj asks sharply. "That doesn't make any sense."

"Are you losing it?" Sarela asks him. I am confident the answer is going to be a yes, but I do not turn off the recording for them. That is their duty.

He does not answer; Anna does: "Give me a few, I need to grab some water and then I'll come back and explain. Those tacos were pretty spicy."

He stares at her and nods like a Human at both Sarela and the Human female. Then the recording ends.

**--Ending Expressive Narration of Recording 29--**

---

*At least I delivered and dropped something, unlike Frank Ocean.*

*TBC*
