---
title: Cookie and Session Pro/Cons
description: The benefits and drawbacks of each
date: 5/4/2016
---

[A continuation/vaguely enlightened reflection on a previous post.](http://ssunday.github.io/2016/cookies-and-sessions/)

So. Cookies and sessions. Why would you use one or the other? Well, I did some researched and have compiled some reasons why.

**Cookies**

*Pro:*

* Can be set for a duration of your choosing

* Does not necessarily end when the browser session ends

* Data is not saved in server side so it does not have to be managed

*Con:*

* Stored client-side so the data can be manipulated by a user to ill-effect

* Not as safe for that reason and because cookies can be stolen and injected

* Browsers can restrict or reject cookies, so functionality could fail if the system depends on cookies and the user is blocking them

* Size restriction--can't hold massive amounts of data as it is typically limited to a few kb


**Sessions**

*Pro*

* Data stored server side so it is more secure

* Safer from user manipulation

* Tighter control over the particular data

* Can hold larger sets of data without a limit

*Con*

* Expires when browser is closed

* Server has to deal with keeping all the data


So there are some of the reasons to use or not to use either sessions or cookies. If you want to store login data of some sort, like a cookie saying the person has been logged in, a cookie with an expiration date of some arbitrary long length of time would be best. But the sensitive data of the login would need to remain on the server, safe from manipulation. Sessions are seemingly more preferable, for the sake of being able to be used by the most amount of users, as Cookies can be blocked and deleted by users. But for the case of keeping a person logged in, cookies are still good and there are, as one can experience on various websites, ways of getting around that by having cookies and sessions doing the same thing.

Looking into the benefits/drawbacks of both methods of persisting data was very illuminating. It made me see them in a different light and from other perspectives, especially with the security and manipulating part, which I had forgotten to consider. I don't think one is better than the other in any general-case---they each have their specific uses.
