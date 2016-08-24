---
layout: post
title: New Day, New Problems - Part 2
description: Interface flexibility
date: 7/6/2016
category: recordings
---

*I just realized that one of the previous posts had a sort of spoiler in it--The existence of the Trinity and the One/presence of them a few decades after the current events in the series (books 1-4). Hahahahaaaaaa. They are immortal, what do you expect?*

---

**--Beginning Basic Narration of Recording 8--**

The voice of Lapadj carries the view into focus with a heated: "It does not even make *sense.* The higher up the decision is made the less the deciders actually comprehend what they are deciding upon. It is like they want to fail. It is like ignorance is emboldening to them."

"Their existence is comprised of ignorance. What do you expect?" Sarela asks him pointedly.

"I suppose, more, I suppose," Lapadj mutters completely formal and definitive. He sighs, shakes his head and glances to the left to see Anna approaching with a steaming cup of coffee.

"That was your mistake," Sarela says.

"I know," Lapadj replies and his voice echoes out into the open.

"Good job."

"You know what?" Anna asks merrily as she plops down onto the chair.

"How to implement the interface," Lapadj answers smoothly.

Both Sarela and Anna say: "Nice!"

Anna, however, continues with: "Want to do it?"

"Sure...but don't we need tests?"

"Can't really test an interface directly, so we just have to make the interface and make sure the existing tests pass."

"A-okay."

He seizes the keyboard and creates a new Java file. Instead of selecting class he selects `Interface` and names it `DataType.`

Before typing out anything else, he opens up the `PostgresData` file and looks at the methods already created in the file. One by one he copies and pastes their declarations into the `DataType` file and trims them into the format needed for an Interface.

It ends up looking like:

```java
public interface DataType {
    void addPost(int id, String title, String content);
    void updatePost(int id, String newTitle, String newContent);
    String[] getPostByID(int id);
}
```

"Seems okay to me," Anna says. She takes the controls for just a moment to make it so the `PostgresData` is implementing the `DataType` interface. Then she runs the existing tests and they continue to pass. "Nice!"

"Thank the Gods," Lapadj murmurs, again, without the power of the audio masking.

"Oh, you're polytheistic?" Anna asks, clearly interested. "What religion?"

Lapadj seeks out the presence of Sarela for assistance. Silence is returned for a short few moments. Then she speaks up with: "Polytheistic contemporary Human religions....Hindu?"

Lapadj replies with: "Hindu."

"Wow, that's...that's really interesting." Anna stares at him for a long while. Then she returns to the computer and commits their changes and responds to the Human who ordered them to perform the modifications. "Ugh, I guess onto the next suggestion?"

"Yes, please give me one moment, though," Lapadj says and rises up and scurries away.

"Yeah, we need to figure out a better way to do this," Sarela agrees and they seek refuge in the supply closet for a second time.

**--Ending Basic Narration of Recording 8--**

---

*To Be Continued.*
