---
title: Multiple Ruby-s
description: Bending over backwards to get things working
date: 16/5/2016
---

Okay so we needed a specific version of Ruby to get old gems and code compiling at a base system level. `1.9.3` something or other. But we had users that needed specific ruby versions, like `2.3.0` so *their* code could compile. It's a weird layering, but we needed it. So begins the balance of multiple ruby versions.

How did we accomplish this dance?

* Used `ruby-install` and set the base system to `1.9.3` ruby version. Installed the specific (old) gems.

* Installed rbenv and set the local ruby version to whatever on the user path that needed it (`/home/user/`). Reinstalled `bundle`, as a copy had been installed in the system level so we needed bundle for *that* particular version of ruby using rbenv.

* Prefixed commands that used bundle/ruby with `rbenv exec` to specify to use rbenv's ruby version instead of default system.

That is the gist of it. Performed through packer and Chef to create a server that has this ruby versioning set up. It works.
