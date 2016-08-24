---
layout: post
title: Enlightenment through Storage - Part 6 - The End
description: Attaining imperfection
date: 2/6/2016
categories: recordings
---

*And by end I mean of the Enlightenment-through-Storage series. This isn't ending any time soon.*

*FYI: The Spine is growing more and more aware of the stupidity of this entire quest along with our intrepid protagonists.*

---

**--Beginning Basic Narration of Recording 6--**

"What if instead of recording through me we do it through some object, such that it would not be completely bizarre if you stared it for prolonged periods of time?" Sarela asks, the recording coming to life with the sight of Lapadj as a Human attaining a cup of Human 'coffee.' He is standing next to a counter, alone except for the invisible, intangible presence of Sarela and the distributed recorder.

"That would be awkward. This is more flexible," he responds, and then takes a sip of the dark liquid. His face scrunches up as he swallows it down.

"Disgusting?" Sarela inquires. "I always wonder how you organics tolerate being able to ingest liquids and solids into your forms."

"I wonder the same thing," he says. "I regret nothing in having only consumed souls for my existence. This is not pleasurable."

He takes the cup of swill and pours into a metallic sink right as Anna walks in. She waves at him.

"Hi!" Anna calls out to him as they shuffle over to meet each other. "Not a coffee fan, eh?" She glances at the emptied cup of coffee beside 'Harrison.'

"No," he answers bluntly.

"Well, some people drink tea instead. I usually lay off the caffeine and coffee this late in the day so I can get to sleep better," Anna casually chit-chats.

"Sleep. Another basic necessity of primitive organic life. Gods, being non-organic is a blessing," Sarela murmurs. "You should reincarnate as a Mechanicha."

Lapadj hums at both females.

"Speaking of that, I think we can finish refactoring before the day is done, so let's get back to work," Anna says and turns to head back to their workstation.

Sighing, the duo of Empirians follow after her. They pass by other dull Humans sitting at equally dull chairs and working on primitive computers. These machines are of a simplistic nature and do not hold the same power and awareness as products of the glorious Empire. Yet the Humans rely on them and thus Lapadj and Sarela must use them.

Anna and 'Harrison' sit down at one of these machines, a shiny metallic one they had been using. This one has a partially eaten fruit known as an 'apple' on the back of it, corresponding with its brand, or 'guild' name of 'Apple'. Humans enjoy using names for simple things to describe more complex things, hailing from the naming of the planet Earth as the element.

Not pondering on any of this, the Kharatzara Lapadj takes the keyboard, focuses in on their programming code, and stares at the screen as Sarela stares at the screen and the two.

"We are eli-" Lapadj stops. "Removing duplication." He says those two words light and fluffily.

"Yeah..." Anna says, voice barely above a whisper as she takes the mouse and scrolls up and down to view multiple parts of the code. "So...we have multiple areas where we do `execute` with our string query on our created statement. Maybe we should pull out that into a separate function. Like pass the query in and then it'll execute it."

"That would make sense, except for the instance where we need a `ResultSet` from its execution." Lapadj points to the spot on the flat screen.

"Ahh, yeah. Well. Maybe we have it return a `ResultSet` regardless and each function can determine whether to use it or not. It would really cut down on the code duplication and isolate where the Postgres driver work is being done."

"Sure."

Anna pauses for a moment and then says, "Do you want me to do it?"

"Sure."

"Ok."

A paltry minute or so of boring staring passes with no quip or comment.

Anna finishes up and turns to Lapadj. "What do you think?"

```java
private ResultSet execQuery(String query) throws Exception {
    ResultSet resultSet = null;
    Statement st = connection.createStatement();
    st.execute(query);
    resultSet = st.getResultSet();
    return resultSet;
}
```

"Looks fine." He motions to run it and she does but it does not work.

"Oh. Yeah. The exceptions." She nods multiple times. "So if we throw an exception in a function and call that function elsewhere we need to throw it there too. And so on."

"That does not seem...wise," Lapadj states.

"It doesn't." She hums.

"Why not deal with it there?" He motions to the execQuery function. "Catch it or whatever right in there?"

"That's a good idea." She gestures for him to use the keyboard.

He blinks once and performs the changes needed in a short time span.

```java
private ResultSet execQuery(String query){
    ResultSet resultSet = null;
    try {
        Statement st = connection.createStatement();
        st.execute(query);
        resultSet = st.getResultSet();
    }catch (SQLException se){}
    return resultSet;
}
```

"Yeah, and let's test-"

He runs the tests. They are green: passing.

"I believe we have removed most of the duplication. Are we finished?" Lapadj asks with a sigh.

"I think so." Anna nods as she looks at it. "Well, we'll see if others agree, I'll make the commit and all that."

"Good."

She finishes typing and then pulls away. "Wow, the day really flew away." She looks at people leaving the building and begins to get up. "I'm going to head out too. Good work today. I wonder what we'll be doing tomorrow."

"I also wonder..." Lapadj murmurs as he rises and heads out. "Good bye." He does not even bother to turn to look at her. Sarela follows after him.

Anna calls back with a muted: "Bye."

A few seconds later of intense walking and breathing and Lapadj and Sarela are in outside world of Earth.

"Well?" Sarela asks. "Day one. Tell me your thoughts. Tell *us* your thoughts."

"This world is a miracle," he answers and then walks away from her. Sarela trails after and then the view goes black.

**--Ending Basic Narration of Recording 6--**

---

*TO BE CONTINUED DUH DUH DUUUUHH*
