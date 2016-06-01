---
layout: post
title: Multithreading a Java Server
description: Allowing it to do multiple things at once
date: 26/4/2016
---

Another part of the tests I was supposed to pass with my Java HTTP Server was making it be multithreaded. Basically making it so it can handle multiple requests at the same time.

With the power of Java libraries, and Java in general, this actually isn't that difficult. Java has a few core libraries to make multithreading possible and using them is quite simple.

The main gist of the implementation of multithreading in Java is to, well, implement a runnable object that has a run function. What is in the run function should be what you want to multithread or have run concurrently. Why are we doing this? So when you make a new thread or use an executor, the program knows what to run on that thread.

So in the loop or wherever you would like to call the run function, you have to either make a new thread for each time you want to call the run function on a different thread, or just use an executor service instance. I used the latter.

An executor service instance is created with a thread pool to run the program on. It can be fixed or cached. I used fixed because I knew I wanted only an 8 thread pool.

```java
ExecutorService threadPool = Executors.newFixedThreadPool(8);
```

And then, to use the runnable and to have the threading occur, have the executor service execute the instantiated runnable like this:

```Java
ServerRunnable runnable = new ServerRunnable(socket, port, baseDirectory);
threadPool.execute(runnable);
```

Or whatever the runnable looks like. Call this as many times as you want (within reason) in a loop of some sort or whatever. That is it, basically. Except for closing it down--when you want to close it down at whatever point call `threadPool.shutdown();` and that'll do it. Overall pretty simple.

I thought it would be harder, but Java really makes it easy. Thanks, Java.
