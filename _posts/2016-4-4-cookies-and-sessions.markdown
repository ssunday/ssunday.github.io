---
layout: post
title: Cookies vs. Sessions
description: Differences between the two
date: 4/4/2016
---

Cookies and sessions are two different ways of retaining data when a client and server begin interacting. Below is a relevant picture describing this general process.

![transfer](/assets/post-images/client-server-computing.jpg)

The session keeps the data locally on the server side, but when the client initially requests and the session is creating, a unique key is given to the client so the server has a way of locating that data. No actual data asides from the key transverses from the server side to the client side and vice versa.

A cookie, however, *does* do this. Cookies can carry the data between client and server. They also have a specific key attached to it for security reasons and can be set to expire after a certain time.

The benefits of a session are that they are not being set back and forth and it can simply accessed locally. It is lighter weight for the client, but the server takes the load of keeping track of all the data and it can potentially get messy. Cookies make this process tighter by having all the essentials be mobile and created only for a set duration and purpose.

They each have their value and purpose. Both can do the same thing, essentially, but depending on the context it might be best to use one over the other.
