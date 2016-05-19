---
title: Systemd Services
description: Launching unicorn with a Daemon
date: 18/5/2016
---

To use systemd one must use service files to run the particular script. These 'services' can be slightly unwieldy. But they do eventually work. We were trying to get a service to start up a unicorn process with rbenv.

Our service file came to work something similar to this (pretend the capitalized words are something meaningful):

```
[Unit]
Description=APP_NAME_OR_WHATEVER_YOU_WANT

[Service]
Restart=always
Type=forking
RestartSec=10
TimeoutStartSec=0
User=APP_USER
Environment=HOME=USER_HOME
WorkingDirectory=APP_DIRECTORY
PIDFile=WHEREVER_PID_FILE_IS
ExecStart=/usr/bin/rbenv exec bundle exec unicorn -c UNICORN_CONFIG_FILE -p APP_PORT -E PRODUCTION_ENVIRONMENT
```

It took awhile for us to get there, but we got there. There are a bunch of similar Daemons out there that look basically the same, as they serve the same function of starting unicorn. Others didn't necessarily use rbenv so that is why this one is mildly special. The `systemctl start SERVICE.service` command must also have an `&` at the end so it runs in the background. Or you could not and just switch to a new tab or something but that seems a bit excessive.

There really wasn't much information on what each service file part did with regards to unicorn/nginx. It was a bit of a journey getting to this point because of that. Lots of trial and error. But in the end it works and that is what matters.
