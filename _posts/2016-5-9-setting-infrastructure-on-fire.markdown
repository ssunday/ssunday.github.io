---
title: Setting Infrastructure on Fire
description: Taking out the trash
date: 9/5/2016
---

Okay so for the past couple of weeks myself and another been wrestling with an infrastructure set up for deploying in-house apps. The point of it was to set up a staging environment for another app. That was all that we wanted to do. Simple, right?

Not really.

Why?

The main reason, the black gangly root cause of this tree of pain and suffering, was an outdated, poorly designed infrastructure set up. It was made in 2012 and that was really the last time anything has been done with it. The infrastructure uses a templating system for provisioning servers with Chef that any derivative forks and tweaks. So the problem isn't the infrastructure--it is what it forks. And that thing includes the horrible design of pulling itself down from the github repository and has broken environmental variables so one would have to push to master to see any changes. Which is pretty bad.

So we can't really do anything. We can't even go in and change the root of it because, being a templating system, we'd have to change everything that depends on it. Some of them being projects that are actually using it.

It's a mess.

But there is a light at the end of the tunnel. The light comes from a torch that will be used to set fire to this entire system and rebuild it sensible. You know, use SOLID principles and all the clean code values that we are supposed to represent. Whether this will actually happen or not is unknown, but it looks like the most viable long term option. Sometimes, you just have to burn it all down and start from scratch. Learn from the many, many mistakes.

I'm kind of hoping it happens. The entire system is like rotten food. The stench permeates and lingers. The trash needs to be taken out.
