---
layout: post
title: Clojure is Cruise Control for Cool
description: Problems made simple with Clojure recursion
date: 2/3/2016
---

*The title was originally Clojure RECURSION is Cruise Control for Cool, but I switched it to just Clojure because of the unbroken alliteration.*

Slightly surprising to me was how easy Tic Tac Toe became to set up and create with Clojure. Not Clojure, not really, but recursion and functional programming. Problems were more easy to solve, in my opinion, using recursion than OOD with Ruby. Maybe not easier, but more streamlined and 'neat,' if that makes any sense.

For example of this was my vaguely-clever way of making the game be replayable, or playing multiple rounds and such. How I ended up accomplishing this was basically nesting two recursive loops to run the game.

```clojure
(defn play-game []
  (let [player-one-marker (io/get-player-one-marker)
        player-two-marker (io/get-player-two-marker player-one-marker)
        first-player (io/get-first-player player-one-marker player-two-marker)
        player-one-is-ai (io/get-whether-player-one-is-ai)
        player-two-is-ai (io/get-whether-player-two-is-ai)]
    (loop [player-marker first-player
          other-player-marker (if (= first-player player-one-marker) player-two-marker player-one-marker)
          board (gf/make-default-board)]
        (if (not (gf/game-is-won-or-tied board))
            (do (io/display-current-player-marker player-marker)
                (io/display-game-board board)
                (recur other-player-marker player-marker
                      (get-move board player-marker other-player-marker
                          (if (= player-marker player-one-marker) player-one-is-ai player-two-is-ai))))
            (do (io/display-game-board board)
                (display-end-game-messages board player-marker player-one-marker))))))

(defn run []
  (io/start-game-message)
  (loop [play-again true]
    (if play-again
        (do (play-game)
            (recur (io/ask-if-player-wants-to-play-again)))
  (io/end-game-message))))
```

So the play-game function, well, plays a game. In the let block it defines all the variables used with the returns of the input output functions. Then in the loop block, we actually play the game until it is over. The variables defined are the current/other player markers and the board. The get-move function gets the player's move and makes a new board with that spot taken, and is put in the 'board' slot of the recur so the next iteration has the updated board. When the game is over, the correct message is displayed and the loop is done. For that function.

In the run function, where play-game is called, there is another loop that has to be gone through and it is the one determining whether the player still wants to play. So after playing a game the loop is recur'd with the information of true/false, true if they want to play again and false if not.

It feels so organic. I mean, it's basically two while loops, but it feels so snappy and smooth. Using recursion always makes me feel special or clever or something. I suppose it's the same as the feeling of using macros in code.

I don't know. This is a self-congratulatory post; I just felt like sharing this because I found it really cool and slick.
