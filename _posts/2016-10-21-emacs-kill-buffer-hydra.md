---
layout: post
title: Emacs Kill Buffer Hydra of Power
description: Murdering buffers all the time
date: 21/10/2016
category: "Emacs"
---


I've just started to get into using the Emacs Hydra package by abo-abo, a true saint among Emacs users. [Hydra](https://github.com/abo-abo/hydra) is an Emacs package that allows you to create chained commands. It is kind of hard to explain without a concrete example.

The example I am going to use is the Hydra I made to speed up my workflow (I feel terrible saying that, but whatever that is what it is.) Emacs tend to build up so many active buffers during a session. Like tab addicts. I have tabs enabled on my Emacs config, so this is literally the case. I open so many buffers and then I see all these tabs and cycling through the tabs gets tiresome. I get lost and then I end up spamming `C-x k` over and over again to bring back order.

So I made a Hydra, utilizing the amazing package.

The full code for it is here and on [my Emacs Config on Github](https://github.com/ssunday/emacs-config)

```LISP
  (global-set-key
   (kbd "C-x k")
   (defhydra hydra-kill-buffer
     (:color pink)
     "kill-buffers"
     ("k" kill-this-buffer "kill current buffer")
     ("c" kill-buffer "kill buffer cycle")
     ("a" kill-all-buffers "kill all buffers")
     ("o" kill-other-buffers "kill other buffers")
     ("q" nil "quit" :color blue)))
```

The helper kill-buffer methods are these:

```LISP
  (defun kill-all-buffers ()
    (interactive)
    (mapc 'kill-buffer (buffer-list)))

  (defun kill-other-buffers ()
    (interactive)
    (mapc 'kill-buffer (cdr (buffer-list (current-buffer)))))
```

So how does this work?

When I type `C-x k` a menu opens in the mini buffer. It shows "kill buffers" and all the commands with their 'hints', the second string in each of the lines after "kill-buffers". If I type `k`, it kills the current buffer, `c` enters the typical kill buffer menu, `a` all buffers, `o` all the buffers except the current one. `q` quits the hydra, but you could spam `C-g` like any sane Emacs users.

A more technical explanation of all that:

The command `C-x k` enters the Hydra `hydra-kill-buffer`. With the defined color of `pink`, the hydra can only be exited using `q` or `C-g`. This means you can do typing and other commands while the hydra is active, but if you hit any of the keys that are used, it will execute the command defined in the hydra. The letters are all mapped to the specific function and have a 'hint' or tool-tip attached to them.

It is pretty neat. Now if I want to kill like five buffers in a row, instead of repeating `C-x k` over and over again, I can do: `C-x k kkkkk` and then `q` to quit. I can also move through my tabs and kill certain tabs. Or just nuke everything with `a`. If I feel specific, can use `c` to kill a buffer by name as usual. If I only want the current one, `o` is there for me.

I'm thinking about figuring out a way to kill buffers below or above the current buffer in the stack. Like in a webbrowser you would be able to close all the tab to the right or the left of the current one. But that is the future.

Now I'm killing all the buffers in rapid order. FEAR ME BUFFERS.
