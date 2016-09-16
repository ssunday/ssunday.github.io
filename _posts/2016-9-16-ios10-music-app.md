---
layout: post
title: iOS10 Music App
description: Complaints and Bugs
date: 16/9/2016 16:00
categories: ["iOS", "Apple", "QA", "Bugs"]
---

I used the iOS music app pretty religiously. I have over three thousand songs. The music apps I use are very important to me. I need clear organization, design, and structure to be able to listen effectively.

So when the iOS 10 music app rolled out I was pretty furious.

Why?

* It looks horrible. Look at this:

![The App](/assets/post-images/main_music_pic.png)

* I asked myself if the CSS had loaded or something because it really looks like a webpage that hasn't loaded properly. Takes a ton of clicks to get anywhere. I couldn't find an image of it (wasn't trying that hard), but it also shows banner ads on certain tabs if you don't have Apple Music and you have the show Apple music button off. What trash. Didn't know the built-in music app was freemium. And those tabs are flaky. They appear some of the time. Not all. And when you launch the app, for a second it shows the Apple Music tabs then they disappear. Nice.

* Low information density. As you can see from above, on the album screen you get two albums per row. Two. **Two.** It takes forever to scroll through dozens if not hundreds. Asides from that, they removed seeing the song duration on the song listing of an album or artist. So if you want to, you know, see the song duration to time a walk or something, you are out of luck. Unless, you are like me and have a really good memory and kind of know how long the song lasts.

* Removed features. Can't see song duration. Can't give star ratings (not that I care or cared.) Add to up-next isn't really a thing anymore. What does this app do again? I don't know. They also took away the color-themed album pages. Which is sad because that was visually pleasing.

* BUGGY.

Oh, it is *buggy*. There is one such bug related to "Up Next" that was so large I questioned whether anyone actually QA'd the thing. It is a little bit hard to explain, but if you are familiar with "Up next" and the queue, like I am, then this makes sense.

[Simple explanation of how the queue works in iOS 10 vs iOS 9, as a primer.](https://www.reddit.com/r/apple/comments/52uhzv/ios_10_cant_rearrange_the_order_of_songs_on_the/d7nqrdl)

So the bug is with modifying the up-next order - removing or re-arranging. If you try to do either and you skip a song or the song ends, your changes will be reverted. This happens basically all the time when you have repeat `ON.` A few times with repeat `OFF.` So you can't really modify the queue order, and even if you could the functionality has changed massively, as you can see above. I much preferred the old version as I used it in Shuffle Mode and set up the queue of shuffle to be in an order I thought was better. Yeah, I could use playlists or something, but figuring out playlists out of thousands of songs is way too time consuming and my mood changes all the time so I like seeing a slice of my music options.

Anyway, as for the bug, I logged it with Apple Support on Twitter. They were pretty useless, but at least they tried and I felt better about bringing it up in a semi-official channel.

In the meantime, I'm exploring other music apps that, you know, *actually work and are readable*.
