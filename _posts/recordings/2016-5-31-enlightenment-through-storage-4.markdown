---
layout: post
title: Enlightenment through Storage - Part 4
description: Getting information
date: 31/5/2016
category: recordings
---

*Anddddddd we're back.*

---

**--Beginning Basic Narration of Recording 4--**

"Harrison, are you ready to get back to working on the tests?" Anna asks as Sarela stabilizes her view of her Empirian comrade and the Human female.

"No, but yes," 'Harrison' answers as he looks up from the small display of the Spine he was secretly looking at. The contents of it were current news in the Empire, more specifically, the antics of the Trinity and the One. He shakes his head quickly of it and says to Sarela: "Is it too late to join their fan club?"

"It is never too late," Sarela responds. "Now get back to touring. You should not have allowed yourself the comfort of the Spine--I thought you were trying to be authentic."

"I am," he hisses and then turns to Anna fully. "So yes, this test for getting a post from the database by id. Let us do that."

He grabs the keyboard and begins to type out the body of the `getPostByID` test. It includes a postgres statement that inserts a post with interpolated variables. The assertion line tests whether the function returns an array of the particular title and content.

Anna stares at it for a few seconds and then says: "So we are going to return the post information as an array? Sounds fine to me, but if we start adding more attributes to a post then it'll get harder to know which value is which."

"But we are not there yet," Lapadj points out. "We should design for the moment, and currently arrays are simpler than the alternatives." It is clear that Lapadj is taking great pride in repeating the Human-design wisdom to a Human.

That Human grinned. "Good point!"

"It is."

She clicks run, sees it error out, and she says, "Now lets implement that method." She navigates to the class where all the Postgres information is. She adds the method and starts typing out the contents of it.

"So how we get the information by the particular ID is we use another SELECT statement, but this time we include where id equals the id we passed in," she explains as she shows off the code to 'Harrison.'

```java
String query = String.format("SELECT * FROM %s WHERE id=%s", tableName, id);
```

He nods at it, neck moving stiffly from being not used to the motion. "So that will get post content with that id."

"In theory," she says, and then clicks to run the test, "and in practice!"

"Wonderful," Ladapj drawls out.

"I can feel your excitement," the Szarehan quips.

"I can feel it too," Lapadj replies to her and then focuses on Anna. "We are now onto our last step, yes? Updating posts?" He goes to the test suite and adds the test, concealing his dissaproval.

"Yep."

"Excellent."

Sarela cackles and both the video and audio cut out.

**--Ending Basic Narration of Recording 4--**
