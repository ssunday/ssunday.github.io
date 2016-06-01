---
layout: post
title: Testing Problems with Tic Tac Toe
description: Issues with stubbing session testing
date: 28/3/2016
---

When I was TDD'ing my web Tic Tac Toe game made using Compojure, Stencil, and Ring, I ran into a major hang-up that severely limited how much I could test the app. That hang-up was being unable to stub the lib-noir/ring session that handled conserving input and settings throughout a game play.

[Lib-noir](https://github.com/noir-clojure/lib-noir) is a library that creates a simple front for modifying and getting from Ring sessions. The sessions themselves are hashmap atoms, but I was unable to figure out a way to effectively stub them so I could pre-load information into them and then test certain game features like turns. I even looked out how the library itself tested its code, but it was not using ring mock requests, so there was a difference in the request structure that I could not figure out how to blend to get the particular *wrap-noir-session** the developers were using to get my tests to work.

I tried getting around that by attempting to stub out the core functions with with-redefs-fn on the get and put! methods, replacing them with functions that would get from a defined parameter variable I created, but that did not work. It kept drawing from the created lib-noir session it made, thereby error-ing out because there was nothing in them to act on.

Then I tried re-binding the session variable itself, a *noir-session* variable, but that did nothing just as well because, I think, it regenerated it at the time of running with the wrap-noir-session function or something like that. It kept clearing out whatever was there, even if I *did* stub it out.

There weren't really any libraries I could find that would be able to help with this. The one I *did* find that was, in theory, supposed to mock out these sessions and cookies was deprecated in a way such that requiring it caused errors and the program would not run. So that was out of the question, unfortunately.

So I tested what I could, breaking down the major logic functions into other files and testing them out. I'm currently trying to figure out a way to accomplish more thorough testing somehow, but I am coming up slightly dry in the ideas department.
