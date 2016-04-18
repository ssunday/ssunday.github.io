---
title: Server Serving Design
description: How I designed part of my HTTP server
date: 18/4/2016
---

The basic Java HTTP server I've made can serve a variety of different things. Files. Images. Directories. Forms. A page to display parsed parameters. Logs. And so on.

At first it was simple to just put in the main server class the logic to display the initial type, directory serving, but this was not very open to modification, especially when I was adding in the ability to serve files. The solution I found was actually pretty solid and made adding new 'types' very simple.

I created a 'ServingBase' class that all these file serving or directory serving class inherits from. It has a few core methods--getting the bytes to display, the HTTP code, and the content display type, and valid HTTP request options.

Each of the child classes override these methods. Any specific information that the object needs to serve its particular information is based in through the constructor when it is made in a serving factory. All the main server does is get the particular server from the factory and call the associated methods it needs to call. Adding a new 'type' just requires making a class that overrides those methods and adding a condition to the factory.

I like this design as it made making more Cob_spec tests pass simpler and not as messy to do. The naming is pretty bad, but I still haven't figured out a better name for it.
