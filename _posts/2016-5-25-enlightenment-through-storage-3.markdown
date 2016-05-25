---
title: Enlightenment through Storage Part 3
description: The beginning of the endless cycle
date: 25/5/2016
---

*Yeah.*

---

**--Beginning Basic Narration of Recording 3--**

The scene blimps back into life with Lapadj in a Human 'restroom.' He is staring directly at a mirror, analyzing his own reflection.

"You have to stop making me stop recording whenever you feel like you are going to break cloak and go on a rampage," Sarela says to him, out of sight but not out of mind. "It is ruining the flow."

"I agree," he replies, "but this is so aggravating. How do tourists do it?"

"By being Empirian," Sarela answers. "Be an Empirian and pretend to be a Human. Do not give into their idiocy. Encourage it so it can destroy them so we do not have to."

At that piece of Empirian wisdom, Lapadj tilts his head and nods like a Human at the place Sarela is occupying.

"There you go. Do you want me to make myself seeable by you?" she asks.

"No. This is more authentic," he says and proceeds to walk right through her.

Being a Szarehan, Sarela is not affected. She makes a huffing noise and turns to move with him, capturing his every movements. He exits the restroom and returns to the table where Anna is waiting for him.

"Are you feeling better?" she asks as he sits down and Sarela takes her position.

"A little bit," he answers. "Let us get back to working on these...tests and functions."

"Great. I made a test to see if `addPost` really adds to the database."

```
@Test
public void testAddPostEntersDataIntoTable() throws Exception {
    PostgresData postgresData = new PostgresData();
    postgresData.addPost(1, "A Title", "Content");
    Statement st = connection.createStatement();
    ResultSet resultSet = st.executeQuery("SELECT * FROM posts");
    assertNotNull(resultSet.next());
}
```

"Okay so," Lapadj says as he stares at the code block. "We have created a `PostgresData` object and are adding a post with those arguments. Then..."

"The connection is connecting to our `wiki-test` database, which I defined up above." She points to it.

"Wa--ah."

"You should use a Tyra Tarkush masker," Sarela mutters. "It is painful listening to the holy language being mangled."

Unable to hear the Empirian, Anna continues on: "The connection creates a 'statement' and with this statement we can execute Postgres commands like select or even create table. The result set is what we get back from executing that select command."

"What does the star represent?"

"It basically says to get all the column information for the rows from the posts table. If we said title instead of it it would get all the titles of the posts and so on."

"That is mildly intuitive," 'Harrison' remarks. "And then we test that there are things in the results."

"Yep," Anna replies. She runs the test. It fails. "Okay, now let's get it passing."

"Yes," Lapadj says, "by actually creating it."

They return to their empty `addPost` function. It stares at them until Lapadj begins to type out the same type of code that was in the tests. He creates a connection and a statement. He pauses when he gets to what to put in for the argument for `execute`.

"Add is the command, no?"

"Insert."

He types insert and finishes it up to make it look like:

```java
String.format("INSERT INTO posts (id, title, content) VALUES (%s, %s, %s)", id, title, content)
```

Anna nods her head at it. "Seems good." She leans to run the test but Harrison does it before she can. It passes.

"It works," Lapadj says smugly at both her and Sarela. "The test was extraneous. Through our will it has been made perfect."

"Like magic," Sarela quips.

"Ugh, sure, but now when we make changes we can verify we didn't screw anything up," Anna says.

"Why would we make changes to this?" His eyes flicker across the screen.

"Because we have to add more functionality and then we'll need to refactor," Anna explains. "But it looks good for now, so we'll get to the next function. Getting a post from a database."

"Using our ID," Lapadj adds softly, shaking his head.

"Yeah, that was a good idea." She takes the mouse and uses the keyboard to create another test for the function called `getPostByID`.

Lapadj sighs at the sight of the new test.

"Do you want to take a little break?" she asks him.

"Yes."

He is not looking at her; he is looking at the spot where Sarela is vaguely. Sarela laughs loudly at him. He shakes his head and the recording ceases.

**--Ending Basic Narration of Recording 3--**

---

*To be continued...*
