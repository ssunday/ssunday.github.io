---
title: A Trip Down Serialization Lane
description: Trying to serialize arrays
date: 12/2/2016
---

With Datamapper, one can store objects and arrays simply by specifying the property type as an Object. What Datamapper does with the particular information is it Marshal’s the data into a string when it is dumped in and de-Marshal’s it when it is loaded out. Marshal’ing is a Ruby way of serializing arrays and other information. It is like turning it into a YAML object or the like, except it is built into Ruby. Datamapper does the converting at time of access; nothing needs to be done.

I had been trying to take the Marshal step out of the hands of Datamapper, make the property a string, so prior to storing it into the database, I’d turn the array into a string using Marshal and then when I get it back out of the database I’d load it using Marshal. Doing Datamapper’s work for it, basically.

This was not working, for reasons out of my comprehension. To the best of my understanding, it had to do with the ‘text’ property of Datamapper and how it works with a postgres database. At certain points (not all of them) when I tried to load the string from the database I’d get an error saying the data was too short. Contrary to intuition, from what I read about this error, this occurs when the data is too large for the database cell/column. I never figured out what was causing this problem, but I tried to fix it. It was a murky mess.

To get out of that rabbit hole, it was decided that I should just serialize the array using some other method rather than use Marshaling. This was actually pretty easy. I used .join and .split to convert the array to a string and back. Made functions to do this and such.

So now my code stores the array as a string. It was an interesting ordeal, to be sure. But it works.
