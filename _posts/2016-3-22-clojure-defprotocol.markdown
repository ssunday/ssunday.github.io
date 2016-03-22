---
title: Faux OOD in Clojure with Protocols
description: Using Protocols in place of multimethods
date: 22/3/2016
---

Protocols are another way of tailoring method behavior in Clojure, like multimethods, which I had been using to implement the variety of different data storage methods (like JSON or Postgres). Protocols are kind of like an abstract class, really. They are a collection of methods and functions that are implemented by records, types, or by the extend-protocol function. In the case of my Tic Tac Toe game, it was with records.

Here is how I set up the main 'DataType' protocol:

```clojure
(defprotocol DataType
  (alternate-file-name [this name])
  (clear-all-data [this])
  (read-tally [this])
  (record-player-tallys [this tally]))
```

That is it. All the methods are part of it and the arguments are defined. 'This' has to be put into each of the argument lists as to refer to the object itself. There can be multiple argument lists, apparently, if sometimes multiple variables are taken in and so on.

To implement this abstraction I used defrecord:

```clojure
(defrecord JSON [] repository/DataType
  (repository/alternate-file-name [this name] (use-different-file-name name))
  (repository/clear-all-data [this] (file/clear-file json-file-name))
  (repository/read-tally [this] (read-the-tallys))
  (repository/record-player-tallys [this tally] (record-the-tallys tally)))
```

Repository being the namespace of the file where I defined the defprotocol. Each of the functions being called perform the task--I took them out and turned them into private functions for ease of reading and to make it cleaner.

Unlike multimethods, there isn't a easy way of dispatching which record to use by some arbitrary value. So something has to figure it out and then manually pass around the instantiated record variable. I did this in a separate file using a cond statement:

```clojure
(defn data []
  (cond (= (data-storage/data-type) :json) (->JSON)
        (= (data-storage/data-type) :edn) (->EDN)
        (= (data-storage/data-type) :pg) (->POSTGRES)))
```

The core file calls this function and passes the 'data' record into the functions that will need it. It isn't that pretty, but defprotocols are faster and cleaner to look at, but it requires more tweaking to be integrated with existing code. After doing that, to add another method I could make another record, require the file in the file that creates the record and add another case to the cond statement. That's it. Not as easy as multimethods, to be sure, but it works.

Defprotocols were strange and slightly difficult to figure out at first, but once I understood how they should be used and implemented, I now can see their use and function.
