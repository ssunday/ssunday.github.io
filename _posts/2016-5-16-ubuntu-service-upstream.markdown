---
title: Script Changes in Ubuntu
description: Getting software up to date
date: 16/5/2016
---

Since the base AMIs we are using for the servers are now using a more current Ubuntu version, there are some things that have to be changed in how we provision the servers with Chef. One of those happened to be background scripts. In the older version of Ubuntu they used to be Upstarts, but with this new version of Ubuntu Upstarts are obsolete in favor of Systemd.

[This website has a pretty good comparison and breakdown of the two.](https://wiki.ubuntu.com/SystemdForUpstartUsers) Their script/service files do not look alike. Their extension is different, too. Systemd uses .service whereas Upstart uses .conf. So to use the script we had to convert the .conf to a .service. We haven't gotten it working fully, but that is because the underlying script for it doesn't work either (at the moment) and the Chef block that *would* start it up and enable it is ancient and *before* the major shift away from Upstart. So the Chef `service` block might not even work with Systemd so we'll have to find a work around for it.

It's kind of interesting that something fundamental like that changed. But annoying that we have to go in and try to figure out how to get something written four years ago to function in a patchwork environment of new and old. Legacy code, eh.
