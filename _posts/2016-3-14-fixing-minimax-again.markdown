---
layout: post
title: Minimax Redux
description: Fixing the TTT AI (again) and getting somewhere final
date: 14/3/2016
---

Minimax is one of those things that is always going to haunt me. I've done it multiple times and when I think I got it I realize I messed up and it isn't as good as it needs to be--it fails in some edge case that I did not think of.

Though, this time, *this time* I think I've got it down (with 99.99repeating certainty).

For this attempt at Minimax, I broke up the functions into pieces and used hash-maps to make everything more readable, which was a problem as I got confused as to whether I was on the max or min side of things. By breaking all these junctions into functions and names with clearly defined paths, I could trace it easier and test it throughout the process. I took inspiration from a variety of different people's minimax codes and pseudo-codes I researched throughout the process to figure out the optimal way of doing Minimax. Together, mixed all together with my own changes and tweaks, I am certain as I can be that I've arrived at the correct solution.

Here is my (current) code ([rest here](https://github.com/ssunday/TicTacToeClojure/blob/master/src/_tictactoe/ai_player.clj)):

```clojure
(defn get-available-locations [board]
  (vec (filter number? board)))

(defn player-markers [ai-marker opponent-marker]
  {:ai ai-marker :opponent opponent-marker})

(defn get-score [board player-markers depth]
  (let [winning-player (gf/game-is-won board)]
  (cond (= winning-player (:ai player-markers)) (- 100 depth)
        (= winning-player (:opponent player-markers)) (- depth 100)
        (gf/game-is-tied board) 0)))

(defn apply-max-or-min [minimax-map player-markers current-player-marker]
  (if (= current-player-marker (:ai player-markers))
      (apply max minimax-map)
      (apply min minimax-map)))

(defn get-next-player [player-markers current-player-marker]
  (if (= current-player-marker (:ai player-markers))
      (:opponent player-markers)
      (:ai player-markers)))

(defn minimax [board player-markers current-player-marker depth]
  (if (gf/game-is-won-or-tied board)
    (get-score board player-markers depth)
    (let [next-player (get-next-player player-markers current-player-marker)]
      (apply-max-or-min (map #(minimax (gf/mark-board-location board % current-player-marker)
                                              player-markers next-player (inc depth))
                              (get-available-locations board))
        player-markers current-player-marker))))

(defn scores-for-available-locations [board player-markers]
  (pmap #(minimax (gf/mark-board-location board % (:ai player-markers)) player-markers (:opponent player-markers) 1)
            (get-available-locations board)))

(defn assign-scores-to-available-location [board player-markers]
  (zipmap (get-available-locations board) (scores-for-available-locations board player-markers)))

(defn get-best-move [moves-and-scores]
  (key (apply max-key val moves-and-scores)))

(defn best-move [board ai-marker opponent-marker]
  (get-best-move (assign-scores-to-available-location board (player-markers ai-marker opponent-marker))))
```

How do I know this works? ~~I don't~~

I know this because I added a mass plethora of tests on the smaller functions I could effectively test. For the best-move function, the function that wraps it all together and spits out the move we really want to know works, I tested all the critical board permutations I could think of, from winning to blocking to general intelligent moves for the first turn or two, which I had been neglecting in previous iterations of the tests for it. Basically analyzing it being intelligent in the beginning and selecting win/block moves in a given scenario. Then I played it many times, because my ability to think up edge-cases in tic tac toe is sorely lacking. I tried out all the cases it had failed on in the past and it actually worked this time. And I lost many times and tied even more. The tests from the previous iterations that failed passed. All together, created my certainty.

It *works.* I feel decent.
