---
title: Assimilating with Clojure
description: Clojure from a LISP perspective
date: 29/2/2016
---

I’ll start off this post by not talking about programming, but my personal programming history. My first language was Python, then I learned Java and Common LISP concurrently. Recently, I took a C++ class and, of course, have been doing Ruby.

So, with learning Clojure now, I’m taken back to my ‘roots’ so to speak or something, considering LISP was an early favorite of mine. At first, I didn’t really like Clojure. The uncanny valley affect plagued me. It was like…LISP…but *not LISP.*

It really felt like this:

![LISP POV] (http://ssunday.github.io/assets/post-images/lisp_views.png)

Definitely Locutus. But I assimilated, eventually, after getting into the process of making tic tac toe with it. Once I started thinking LISP again and pretending it was basically a tweaked LISP, all my dislike went away. I began to abuse recursion to make life easier. I still think LISP does recursion better, but we can’t always win. Happy to be back to Polish Notation, though. Parenthesis are nice, too.

Definitely Locutus. But I assimilated, eventually, after getting into the process of making tic tac toe with it. Once I started thinking LISP again and pretending it was basically a tweaked LISP, all my dislike went away. I began to abuse recursion to make life easier. I still think LISP does recursion better, but we can’t always win. Happy to be back to Polish Notation, though. Parenthesis are nice, too.

The one thing that bothers me about Clojure, specifically, is the changing of cons/car/cdr, or well the modification of the previous and the elimination of the latter two. In LISP, cons creates a, well, cons cell with the two supplied arguments.

```LISP
(cons 1 2)
(1 . 2)
```

In LISP, all lists are made up of cons cells, two element collections. The first and the rest. To query for this, you can use car and cdr. [They are named for the machine lingo of the IBM computer.] (https://en.wikipedia.org/wiki/CAR_and_CDR). You get the first element, a value, and then the rest, another cons cell.

But Clojure doesn’t have any of that and cons works differently. It takes an element and a *sequence* and smashes them together. So the above LISP code does not work. Which is annoying, and I had to wrap my mind around the change in what cons means in Clojure.

But asides from that, Clojure is alright. So far, anyway.
