---
layout: post
title: Tic Tac Toe Menu Refactoring
description: Creating a command-pattern-style menu in Clojure
date: 7/3/2016
---

I was at a junction with the Tic Tac Toe project where I needed to add a menu option at the start to ask the user if they'd like to see previous game scores or play the game. I added the option easily enough with a simple input/output query and if/else block, but it felt tacky. So I did a bunch of refactoring and decoupling to implement a pseudo-command pattern.

I took the options and put them in their own files. The display previous scores and all of the game running functions were siphoned off. The menu file had a map of the numbers and options, for ease of displaying. Then I created a cond statement to call the respective functions that were required at the top. I'm trying to figure out a better way than cond, but it works and the code is a lot neater. I wanted to do this so the user could play a game and then see the scores again or something like that. Also if more options were to be added, they can be added much more easily now with this refactoring than before.

Here is what the game menu file looks like:

```clojure
(def game_menu {1 "Play Game"
                2 "See Scores"
                3 "End Application"})

(defn get-menu-options []
  game_menu)

(defn do_menu_option [option]
  (cond (= option 1) (run-game)
        (= option 2) (display-previous-scores)
        (= option 3) true))
```

Run-game is the function that calls the main game loop with playing with different input or same input. I might do more work on it if I get an epiphany, but it gets the job done for now.
