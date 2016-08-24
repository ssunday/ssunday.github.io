---
layout: post
title: Healthy Ideas - 2
description: Actual Clojure
date: 22/6/2016
categories: recordings
---

*I'm turning into one of those fanfiction authors who have notes before a chapter that are the same size, if not longer, than the chapter itself. I'm trying to stop myself. I really am.*

---

**--Beginning Basic Narration of Recording 15--**

"We are back," Sarela states to whoever is viewing these recordings. The recorder is focused onto Lapadj's scowling face and Grapefruit's impassive fruity flesh.

"Great," the Goddess says. "Who are we recording these for?"

Her extremely relevant question is met with a snicker from Sarela and a scoff from Lapadj.

"Empirians," the Kharatzara mutters as he looks off into the distance where the entrance to the kitchen is. Anna has yet to return to being by him. He swivels side to side in the chair.

"He is not wrong," Sarela says.

"I do not think he could be with that answer," the Goddess says. "Whoever is watching this might decide to worship me or remember that I exist because of this. A small, probably vain, hope, I know, but *maybe.*"

"Maybe," Sarela repeats.

"Finally," Lapadj mutters as Anna comes into viewing. She is coming towards them with a clearly full cup of coffee and glass of water.

"Hi," Anna says as she begins to settle down. "Sorry, I bumped into Mark and we talked for a little bit. I also got you a glass of water. I don't see you drink that much and I didn't want you to get dehydrated or anything."

"Yes, she would not want you to get *dehydrated* or anything," Sarela mockingly says. She chuckles softly as Lapadj stares at the water glass. "Humans."

"If you wanted me to stay hydrated, you should have just offered me your soul," Lapadj states aloud, as in aloud to all persons, Anna included. Not loud enough to carry across the room, but loud enough for Anna to clearly hear it.

And she does. Her eyes widen. Sarela gasps and makes a little shriek as soon as she realizes what Lapadj did. The Human's dark tan skin becomes a shade lighter for a flash of a moment and then she begins to giggle.

"Harrison, I never thought you were the joking type," Anna says. "That joke was something like Mark would say. You guys should meet up sometime."

"Perhaps," Lapadj says, forcing a smile to reinforce that he was joking with his previous remark.

"Lapadj, you are an imbecile with incredible grace," Sarela speaks, voice calm, reeling from being on the verge of hysterics. "If you had not been so weird and awkward with her since the start of this, you would have definitely earned the ire of the Distortion Field, some nearby Sacon, or a devoted Empirian. Or all three."

"Anyway," Anna says, "let's get to work. How is Vim treating you?"

"Let's use IntelliJ like you originally intended," Lapadj evasively answers and launches IntelliJ from the dock.

"Sure, yeah," Anna responds, shifting in place. "So parsing a base 64 binary string."

"Why are we doing this?"

"It is how we are transferring data for our systems, I think," Anna says.

"You think."

She shrugs. "Does it really matter? We need to take a string and parse it."

"I suppose it does not," Lapadj whispers to himself and to the recorder. "I am unfamiliar with Clojure, please begin."

"Sure, yeah." Anna begins typing out the base of the function.

```clojure
(defn parse-base64-string [base64-string])
```

"So that is the function we'll need to make. Now we need to make a test." She creates another file. "We use Speclj for testing Clojure code. Here is what it generally looks like..."

```clojure
(describe "parse-base64-string"
  (it "returns parsed string"
    ))
```

"So in the `it` block we have a `should` statement that will test something. The describe is basically the function and the it is what we want it to do specifically."

"Okay," he says in response to her explanation. "So the test should be whether the parsed string is equivalent to the string that we converted to base 64 and gave to this function."

"Yeah, that sounds right," Anna says.

She begins typing and ends up with a partially completed test case.

```clojure
(describe "parse-base64-string"
  (it "returns parsed string"
    (let [original-string "Hello World"
          encoded-string "Something Encoded"
          parsed-string (parse-base64-string encoded-string)]
      (should= original-string parsed-string))
    ))
```

"Now we need to encode `original-string` to base64 format so we can test it," the Human says. "A website can probably do that for us."

She looks one such 'website' up and finds one that did. She encodes the string and copies it into the test case. It, of course, fails.

"Now to writing the function!"

"Great," Lapadj murmurs. He stares at the water and makes a motion to reach for it and in doing so he knocks Grapefruit onto the floor.

"Oh, don't worry, I'll get that," Anna says as Grapefruit makes a dull scream.

"No, I will," Lapadj says quickly and makes the same motion and then their heads collide.

"Idiots," Sarela says and she cuts the recording off.

**--Ending Basic Narration of Recording 15--**

---

*To be continued.*
