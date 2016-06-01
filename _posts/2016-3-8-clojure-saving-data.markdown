---
layout: post
title: Saving Data to a File in Clojure
description: Finding better ways to do the same thing.
date: 8/3/2016
---

Another feature to be done with my Tic Tac Toe Clojure project was to have the win/loss/draw tallies persist between application runs and for the given player's scores to be displayed as a cumulative total count rather than each match up's total.

This was a sticky problem, because I had been just saving a single integer and name to a .txt file with the spit/slurp commands of the java.io fame. I tried doing complicated regular expression ninjitsu to parse the wins/losses/draws and name from the .txt file but it was an up-hill battle because string splitting and partitioning and all that gets messy fast. For me, anyway.

My salvation came from an outside source--another Human being. Gasp. They suggested that I use the [.edn file format](https://github.com/edn-format/edn), a fancy way of storing data in its natural form that is something like a .dat file. Basically, it would make my life much simpler as instead of converting to a string and then back out I could just spit the map and get the map back out.

And it did. EDN is great. What was a mess is now a very simple set of methods to do everything I needed it to do.

```clojure
(defn record-tally [player-tally]
  (doseq [player player-tally]
    (spit player-tally-file-name (prn-str player) :append true)))

(defn read-tally []
  (if (.exists (file player-tally-file-name))
    (with-open [rdr (reader player-tally-file-name)]
      (map #(edn/read-string %) (doall (line-seq rdr))))
    nil))

(defn read-total-tally []
  (let [tally (read-tally)
        total-tally (atom (zipmap (player-names) (repeat {:wins 0 :losses 0 :draws 0})))]
    (doseq [tally-set tally]
      (swap! total-tally update-in [(first tally-set) :wins] + ((second tally-set) :wins))
      (swap! total-tally update-in [(first tally-set) :losses] + ((second tally-set) :losses))
      (swap! total-tally update-in [(first tally-set) :draws] + ((second tally-set) :draws)))
    @total-tally))
```

Also through this process I learned that when you are using with-open and line-seq due to the nature of lazy-seq, sometimes the line-seq of the entire file is not fully loaded or completed when the stream closes, you get 'stream closed' errors. Which is frustrating, but that is what doall is for, in case anyone was wondering why it was there in the read-tally function.

So. .txt--good for small stuff. Not so good for more complicated lines of data. EDN is the way to go.
