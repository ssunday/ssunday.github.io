---
title: Struggling to Name Things
description: A mild problem in server design
date: 19/4/2016
---

So with my Java Server I have these series of classes that are responsible for controlling the server routes. They get the bytes to display and know which http code they are and their content type and so on. The problem I had with them was what to call them.

Controller seemed a bit obscure, so I tried something else. At first I had called them RouteTypeServing. That wasn't that much better, to be honest. It isn't really a noun or something very understandable to a general person.

So I switched it up with 'Deliverer.' This works slightly better as it is more of a metaphor and is more/less concrete. These classes deliver the information that the server serves. It makes sense. The only problem I have with it is that it isn't that easy to say, for me at least. Asides from that, it holds well enough.

I'm trying to think of other, better naming schemes for the system, but I'm drawing blanks. This type of vaguely abstract naming is not my forte. At least I found an improvement.
