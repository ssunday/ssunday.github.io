---
title: Versioning Mess
description: An ongoing ordeal
date: 2/5/2016
---

I'm working on a project where we are trying to provision and setup a Ubuntu environment with a specific version of [Chef](https://www.chef.io/chef/). A version of Chef that is three years old and extremely outdated.

This is causing quite a mess because it needs a particular version of JSON that is also outdated and will not compile due to a change in either gcc or ruby. We tried to go back to an earlier gcc version, a different JSON version as much as we could, a slightly more updated version of Chef, and now we are trying a different version of ruby to see if that can fix it.

It is exhausting and crazy. The entire problem came about because the infrastructure we are relying on did not update or change when its dependencies did, so it is so far behind we have to bend over backwards to try to get it to run. It is madness.

It's almost to the point we are going to have to forcibly update it to the new version of Chef so we can get the environment up and running. It is pretty bad.

Lesson: UPDATE
