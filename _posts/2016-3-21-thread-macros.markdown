---
title: Thread Macros for Improving Readability
description: Using thread macros for readability
date: 21/3/2016
---

No, thread macros do not have anything to do with threading or parallel computing. They are just a Clojure form for 'threading' a expression through other expressions in essentially reverse order so nested structures can become more readable. I went through my tic tac toe Clojure code and found a variety of places to use it in order to improve readability. Improve is surrounded in air quotes in my mind as I prefer Polish Notation. I don't know, it looks better nicer to me, but it is not for everyone. Which is partially why thread-macros are used.

A few lines in question that have been 'threaded:'

```clojure
(-> (read-total-tally)
    (display-tally)))
```

```clojure
(-> file-name
    file
    .exists))
```

```clojure
(-> (* dimension dimension)
      range
      vec))
```

```clojure
(-> board-spaces Math/sqrt int)
```

```clojure
player-tally (-> [player-one-name player-two-name]
                  (zipmap (repeat schema/default-wins-losses-draws-scores))
                  atom)

```

They are not extremely nested so the change isn't that big, but I find that using the -> macro improves readability marginally, and at least removes *some* confusion in certain areas. Makes it less horizontally packed and spreads it out vertically. There were a few points that really made it nicer, namely the last one. I would only use it sparingly, though.
