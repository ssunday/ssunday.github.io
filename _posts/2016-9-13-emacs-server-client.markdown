---
layout: post
title: Moving Emacs to a Server setup
description: no more loading times
date: 13/9/2016
category: "Emacs"
---

This is one of the big leaps of my Emacs configuration: Getting it run as a 'server' with 'clients.' AKA a Daemon. So you load it up once and never again. Great reduction in start up times. Basically, you start emacs in the background and then new instances will be loaded up using the same pool/initialization. Pretty nice.

Getting it working, however, is slightly more complex than just using `emacs --daemon` or doing `(server-start)` within your init or inside Emacs itself. For me, it required a few scripts and UI tweaking.

The script below is from [this person's Emacs setup.](https://github.com/brianm/emacs-client-mac/blob/master/emacs-client-mac.scpt)

```AppleScript
tell application "Terminal"
	try
		-- we look for <= 2 because Emacs --daemon seems to always have an entry in visibile-frame-list even if there isn't
		set frameVisible to do shell script "/Applications/Emacs.app/Contents/MacOS/bin/emacsclient -e '(<= 2 (length (visible-frame-list)))'"
		if frameVisible is not "t" then
			-- there is a not a visible frame, launch one
			do shell script "/Applications/Emacs.app/Contents/MacOS/bin/emacsclient -c -n"
		end if
	on error
		-- daemon is not running, start the daemon and open a frame		
		do shell script "/Applications/Emacs.app/Contents/MacOS/Emacs --daemon"
		do shell script "/Applications/Emacs.app/Contents/MacOS/bin/emacsclient -c -n"
	end try
end tell

-- bring the visible frame to the front
tell application "Emacs" to activate
```

I took that script, saved as an application in the AppleScript Editor, gave it the Emacs Icon, and then just click on it to run it. It starts the daemon if it is not already running and opens a window. To create a new frame of emacs/instance, I made an alias that will use `emacsclient` rather than the regular Emacs. This is that alias:

```
alias em='/Applications/Emacs.app/Contents/MacOS/bin/emacsclient -c -n'
```

The daemon needs to be running for that to work, however.

That seems simple, right? Well, kind of. I run Emacs as a GUI for everything except Git stuff, so there are some...rough edges to sort out with getting the GUI system to work properly. One problem is with using `window-system` to check whether Emacs is in GUI mode or not. Because of how it launches it will think it is in now window-system mode so it'll not execute that code block. And any config that requires graphical-type options will need to be wrapped and executed differently.

The way I discovered how to do this is to do the functions/loading in an `after-make-frame-functions` hook that runs if it is a daemon.

Example:

```Lisp
(if (daemonp)
    (add-hook 'after-make-frame-functions
        (lambda (frame)
            (select-frame frame)
            (load-theme 'atom-one-dark t)
	          (set-frame-size-according-to-resolution))))
```

This works rather brilliantly all together in [my config](https://github.com/ssunday/emacs-config). I'm having some issues with mode-line size, but it isn't something big (heh) for me to ditch the client altogether. It really speeds up launch times and if I make edits with the config, I can try it out by launching a separate process without ruining an existing editing environment. I like it so far.
