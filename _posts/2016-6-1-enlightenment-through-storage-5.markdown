---
title: Enlightenment through Storage Part 5
description: Updating and losing it
date: 1/6/2016
---
**--Beginning Basic Narration of Recording 5--**

The scene resumes with the sound of Sarela quieting down. The Szarehan's laughter slows to silence.

"I am sorry, mushala," she sputters out, still reeling from her giggling, "but that was some authenticity right there."

"I knew I should have found someone else for this mission," Lapadj murmurs and Sarela gives out another burst of cackling. She ceases a few seconds after right as Lapadj nods at Anna while she types out the next test.

"So, the only things that can be updated are title and content," Anna says. "Wouldn't make sense at all for them to be able to change the ID."

"Agreed." Right as Anna finishes making the test and running it to see it fail, he takes the keyboard and begins typing out the function definition and the parameters. "I believe we should pass each post attribute individually for now."

"That makes sense, as you said before," she starts, "we don't have any more information so we should make it simple."

"Yes."

He finishes a few moments later.

```java
public void updatePost(int id, String newTitle, String newContent){
  String query = String.format("UPDATE posts SET title=%s, content=%s WHERE id=%s", newTitle, newContent, id);
  Statement st = connection.createStatement();
  st.execute(query);
}
```

"Nice."

He runs the test and it goes green.

"Nice!" she exclaims. She claps a few times.

Lapadj and Sarela both stare at her, but Anna can only feel embarrassed due to the former.

"The little things, no?" Sarela mutters.

Lapadj clearly looks like he wishes he could click his fingers together and ignite mana that would harm both of his companions.

"What is next? We are done, no?" 'Harrison' inquires.

"No we are not," Anna answers. "We have to refactor this. There is a bunch of duplication here that we should get rid of."

The Kharatzara that is appearing as a Human is gazing at Anna. His brown eyes lock onto her form and squint just slightly. Sarela focuses onto the scene, allowing an excellent view of the look he is giving to the Human. It is unwavering in its stillness.

"The universe has a multitude of duplication," he says, "but that does not mean we should exterminate it. Even if we may want to."

Sarela switches to Anna right as she blinks. She draws in a gulp of breath. "Well. Um."

"If you wanted to say that all Humans should be exterminated, you should have just said it," Sarela chimes in. "Or were you referring to the Sacon? Either one works..."

"I was thinking Humans, but the Sacon might be a better option," Lapadj replies. "Without them there would be no great pressure for us to be cloaked and I could just do as I pleased."

"But that would go against the point of this mission, no?" Sarela questions drolly.

"Yes." Lapadj turns to the recording device. "I apologize for all statements I have made that contain contempt for Sacon and the Contract of Sangrae La. I blame Humanity."

"Nice."

"Um." The voice of Anna draws the two Empirian's focus back to her. The scene locks onto her face. "What are you looking at?"

The view chips away as Lapadj answers stiffly with: "Nothing."

**--Ending Basic Narration of Recording 5--**
