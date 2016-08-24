---
layout: post
title: No Such Thing as Being Alone - 2
description: Alone? What is 'Alone?'
date: 19/7/2016
category: recordings
---

*"I have lost control of my life" - thought by literally all of my characters at some point.*

*For King Fla'neiel, this is thought basically 95% of the time. For Sarela, her percentage is steadily rising due to her proximity to has-no-chill Lapadj.*

---

**--Beginning ~~Basic~~ Expressive Narration of Recording 24--**

"So we need to add the TinyMCE script to the top of the file to make it initialize, no?" Anna asks. She is squinting and blinking at the screen, playing around with the file.

"That is how the documentation describes it, yes," Lapadj replies, in full clarity. His pale face is no longer splotched with red.

"Finally, clarity," Sarela murmurs, "is it not nice to be able to record something worthwhile?"

"You were not recording him when it was hard to understand, though," Grapefruit points out verbally.

Sarela makes a hushing noise at the Goddess. She complies easily.

"So we can just put it up above this Mustache template," Anna says.

"To start we should copy and paste in the default initialization of it," Lapadj says, "to make sure it works simply."

"Good idea." She does exactly that.

```html
<script>
tinymce.init({
  selector: '#mytextarea'
});
</script>
```

Then she opens up the page they are changing and they can visually see that it is not changing anything.

"Hm," Anna says at the code's failure. "Oh! We need to change the selector to an id or class that the textarea is using. Let's make it content."

"Ahh," Lapadj drawls out as she makes the slight change.

With that modification, the TinyMCE editor appears on the screen with all its many extraneous options. A cheer is elicited from them in each their own way.

"Lapadj, I am beginning to think I have no idea who you are," Sarela says dryly.

"Can one ever?" he retorts with an awkward sly grin.

"No, not really," she concedes.

"Okay so now we need to set it up to meet the requirements, yeah?" Anna asks.

"**Bold**, *italics*, and <u>underline</u>, if I remember correctly," Lapadj says. "I also think we should get rid of that top bar with all those options. It is ugly and serves no purpose."

"Yeah, I agree. Also the bottom bar too...The users really don't need to see the details of the formatting. We just need the main three in a bar so they can select it. That's it."

After they engage in the act of typing out the lines of code needed, going back and forth between the editor and the documentation for TinyMCE for quite some time, they render the page that now contains the condensed editor that fits the specifications desired from it. The javascript code that performed this is:

```javascript
tinymce.init({
  selector: '#content',
  toolbar: 'bold italic underline',
  menubar: false,
  browser_spellcheck: true,
  statusbar: false,
  entity_encoding: 'raw'
});
```

Anna demonstrates its ability to save information into the database by clicking save and retrieves it a few seconds later. "It'll save the HTMl version," she says of it.

"Is that a problem?" Lapadj shifts in place.

"No, that is what we want." Her voice is clearly unsure of that statement, but Lapadj smirks at it.

"Very good. Commit, push, and make a pull request?" he asks with surety she did not have.

She responds with a nod. He proceeds to type in all the respective git commands necessary without error. Following that, she revolves around in her chair to gaze at the clock on the wall, ignoring the one in the corner of the large computer screen.

"Wow, look how time flies," she says. "Want to have lunch with Mark?"

"Yes," is the immediate response from Lapadj. Sarela and Grapefruit both say the same thing, although the Human cannot hear them.

Anna gets up and Lapadj copies her.

"Lapadj, before you meet the new Human, I have some advice," Sarela says to him as the recording ends.

**--Ending ~~Basic~~ Expressive Narration of Recording 24--**

---

*Time is an illusion. It goes at a rate I say it does.*

*TBC*
