---
layout: post
title: "Comparing Common LISP and Clojure: Cons Cells"
description: "(Cons . Cells)"
date: 24/1/2017
categories: ["Coding", "Clojure"]
---

The existence (or lack thereof) of cons cells in Clojure might be one of the first things LISPers notice when switching to Clojure. It was for me, anyway. In Common LISP and other LISP languages, cons cells are two element structures that are the basis of all lists and essentially the programming language itself. In LISP, to create a cons cell, simply use `cons` with the two elements:

```LISP
? (cons 1 2)
(1 . 2)
? (cons 1 '(2 3 4))
(1 2 3 4)
? (cons '(1 2) '(3 4))
((1 2) 3 4)
? (cons 1 nil)
(1)
? (cons nil 1)
(NIL . 1)
? (cons nil nil)
(NIL)
? (cons nil '(2 3 4))
(NIL 2 3 4)
```

The two elements can be anything. Two things, two lists, a list and nil, nil and something, and so on. To access the elements of a cons cell, you can do `first` and `rest`, if you want to make your code easy to understand for newcomers, but the typical way of doing it is `car` and `cdr`.

Which don’t sound like much of anything. CAR? CDR? What do those even mean?

Here’s a quick trip back in time: The early LISP languages [were built on old IBM computers that had particular word instructions to access values of a 'register' or machine location.](http://www.iwriteiam.nl/HaCAR_CDR.html) The left half of the register was the address and the right half the decrement. So the LISP way of quickly accessing these values became `car` and `cdr`. Respectively, they meant: "Contents of the address part of register" and "Contents of the decrement part of register." And so `car` and `cdr` were created to get the first and rest part of a structure. `first` and `rest` came into being eventually, but `car` and `cdr` stuck around because they were fixtures in the language. Everybody used them. You can't take them away.

But Clojure did. Clojure only has the less-obscurely named and rather dull `first` and `rest` to achieve those essential accessing functions.

Yet Clojure did not purge all the oddly named LISP functions. There *is* a method named `cons`.

It doesn't make a cons cell, though, not really. It merely takes something (anything) and prepends it to the given *sequence*, returning it as a list.

```Clojure
user=> (cons 1 2)
IllegalArgumentException Don't know how to create ISeq from: java.lang.Long  clojure.lang.RT.seqFrom (RT.java:542)
user=> (cons 1 '(2 3 4))
(1 2 3 4)
user=> (cons '(1 2) '(3 4))
((1 2) 3 4)
user=> (cons 1 nil)
(1)
user=> (cons nil 1)
IllegalArgumentException Don't know how to create ISeq from: java.lang.Long  clojure.lang.RT.seqFrom (RT.java:542)
user=> (cons nil nil)
(nil)
user=> (cons nil '(2 3 4))
(nil 2 3 4)
```

So the one thing you really cannot do with it is use `cons` with a single element as the second argument. In LISP you can, as you saw in the base example up above that created a dotted list. That doesn’t seem like that jarring of a shift. Just a few use cases! But the entire *name* of the method is a lie. Clojure isn’t making a true cons cell. The difference in the meaning of the function `cons` is vastly different. Cons cells aren't the underlying implementation of lists in Clojure. Cons cells have nothing to do with `cons`.

Clojure—by keeping the name and not the substance—is programmatically appropriating from Common LISP for reasons I don't really understand.

It really isn't the end of the world, though, as much as it doesn't make sense. There are far worse things to do in a programming language than keep a bizarre name for something because, well, *that's how it's done*.

...

I suppose Common LISP and Clojure aren't all that different.
