---
title: Pretty Colors with ANSI
description: Colorizing output in Clojure
date: 7/3/2016
---

So with my Clojure tic tac toe game there is, of course, a board. 3x3 or 4x4, in my game's case. On the command line it will display the board in a very simple fashion to show the current state. It looks kind of boring, though. Just plain white on black or black on white, depending on what default color scheme you are using. The point is that it doesn't show a difference between markers and open spots.

![default board](http://ssunday.github.io/assets/post-images/default_tic_tac_toe_board.png)

It could look better. Better as in, having two different colors for open spots and markers to make it 'pop' a bit more. So began my quest to colorize Clojure output. Me being me, I consulted the google overlord, and found a variety of libraries to making output much fancier, including the ability to add color. But it felt a little bit overboard to incorporate an entire library for one simple change, so I began to look at this library that was aptly named ['colorize.'] (https://github.com/ibdknox/colorize)

No, I did not use it. *Directly,* anyway. I looked at its source code and tried to figure out how one accomplishes adding color in the first place in Clojure. I didn't need the libraries methods or other nice add-ons; I just wanted to know how the author used Clojure to colorify output, because the direct answer was illusive to me elsewhere.

The answer was pretty simple, I discovered. How it is done is using ANSI codes that correspond to a color. To  markup the string you use "\u001b" and then the specific color code. To close it, you use another code that 'ends' it. Felt something like HTML tagging.

```clojure
(def colors {:end-marker "\u001b[0m"
                  :default "\u001b[39m"
                  :white   "\u001b[37m"
                  :black   "\u001b[30m"
                  :red     "\u001b[31m"
                  :green   "\u001b[32m"
                  :blue    "\u001b[34m"
                  :yellow  "\u001b[33m"
                  :magenta "\u001b[35m"
                  :cyan    "\u001b[36m"})

(defn colorize-markers [row player-one-marker]
  (map (fn [spot]
        (cond (number? spot) (str (get colors :cyan) spot (get colors :end-marker))
              (= player-one-marker spot) (str (get colors :red) spot (get colors :end-marker))
              :else (str (get colors :blue) spot (get colors :end-marker))))
        row))
```

The colorize library code had a similar colors hash. I condensed the concept with the \u code and only took a few of the colors. It was easier to read if I did it that way, instead of just putting the raw color code, because it was not very...readable. I don't think there are many people who memorize ANSI color codes, and I don't care to be one of them.

The colorize-markers method makes the spot red if it is marked by player one, blue if by player two, and cyan if it is open. Then the other functions add the spacing formatting and then we get this semi-beautiful board:

![colored board](http://ssunday.github.io/assets/post-images/colored_tic_tac_toe_board.png)

Not perhaps the most exciting of problem solving, but with this type of problem it was less on logic and more on *how is this accomplished.* How I accomplished accomplishing it was interesting to me, because I had to sift through another person's code to find the method used to attain this output. Hopefully someone finds this useful so they don't have to go and dig through libraries to do something as simple as having a colored string.
