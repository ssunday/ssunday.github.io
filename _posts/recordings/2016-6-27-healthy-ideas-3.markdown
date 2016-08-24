---
layout: post
title: Healthy Ideas - 3
description: Writing actual Clojure
date: 27/6/2016
category: recordings
---

**--Beginning Basic Narration of Recording 16--**

The scene crinkles into life. Anna and Lapadj are still sitting next to each other. Grapefruit has been placed on a more secure spot of the table. The glass of water has clearly been used in some capacity. Its water level has been lowered.

"Why did you choose to be a spherical object, again?" Sarela inquires to the Goddess currently taking form as a grapefruit. "No. Why did you choose to be something so mundane in the first place?"

"Not all Gods have such tangible forms, or have ever...had the strength to be so corporeal," she murmurs that half-hearted response. Sarela sighs and then makes a muffled clicking noise of affirmation and understanding to that.

"Whatever, it is fine," Lapadj says to Anna. "It being there offers me comfort." He glances at the God.

"Um. Ok." Anna nods. "Well." She puts her hands together. "Let's get to writing that function, yeah?"

"Yeah." Lapadj's Empirian accent creeps into being with that Human utterance.

Swiveling back to looking at the screen, Anna ignites the computer with life. Light comes from it as it awakens fully. IntelliJ is up and set up for their needs. The file that needs the function is awaiting their typing. Lapadj takes the keyboard and assumes the position to begin.

"How can we parse a base 64 binary string?" Lapadj asks Anna, tilting his head.

"I think there is a Java function for it," Anna says. "This is where Java Interop comes into play. At the top of the file we can just import the package that has it."

She takes the keyboard and types out:

```clojure
(:import [javax.xml.bind.DatatypeConverter])
```
"And now we can access the `DatatypeConverter`'s static methods. It has a parse method."

"I see..." Lapadj begins to type out the interior of the function. "What is it called?"

"Parse base 64 something or other. IntelliJ will autocomplete it."

It does as he says. The function appears from a drop down menu and Lapadj selects on it. It appears inside the editor, exactly where he wanted it to be.

A few seconds later he is done and shows off the function to her.

```clojure
(defn parse-base64-string [encoded-string]
  (let [decoded-string (javax.xml.bind.DatatypeConverter/parseBase64Binary encoded-string)]
    decoded-string))
```

"Nice," she says as usual. She opens up the terminal and sees the continuous test run again at their saved changes. The test they added fails at the inclusion of the function. "Not nice."

Lapadj mutters at its failing. "Why does it fail?"

"Oh yeah. That function returns a byte array. We have to turn that into a string."

She takes control of the keyboard and adds a line and a few tweaks.

```clojure
(defn parse-base64-string [encoded-string]
  (let [decoded-array (javax.xml.bind.DatatypeConverter/parseBase64Binary encoded-string)
        decoded-string (String. decoded-array)]
    decoded-string))
```

Glancing at the terminal, it shows the green of the test passing.

"Excellent," Lapadj purrs out.

Anna claps her hands together. "Great. Want to take a little break? Maybe you can eat your grapefruit."

That suggestion inspires the Goddess of Programming to make a little shriek. Anna cannot hear it. She only sees a plain fruit on the desk.

Lapadj, knowing of the truth of this mild all, says: "Sure...I should...eat it elsewhere to make sure I do not make a mess." He rises up, seizing Grapefruit and beginning to walk off.

"Oh. Okay. Um. I'll be in the kitchen. If you'd like to join me." She makes a little gesture and wanders off.

He blinks. "Maybe another time." Then he turns away.

He mutters to the recorder, Sarela, and Grapefruit in his clutches: "We need to figure out a better solution to this."

"Aye ky to that," Sarela says. Grapefruit exclaims the same and the recorder goes dark.

**--Ending Basic Narration of Recording 16--**

---

*Trust me, I know what I'm doing with this Grapefruit thing. I really do.*

*To be continued.*
