---
layout: post
title: Working with Sockets
description: Low level server design
date: 12/4/2016
---

Moving on from the comfortable world of Clojure and Tic Tac Toe, I have started my Java HTTP Server. The point of it being to serve files and show a directory. But that really isn't the point of this post. It is about the most basic part of a server. Sockets!

Okay so basically, from how *I* understand it, sockets work something like this:

A server socket opens on a particular port, say 5000. It listens for incoming connection. When a regular socket opens up on 5000, the server socket can accept its connection. Then the server socket can write/get stuff from that particular socket's connection.

This diagram explains it pretty well:

![Socket Workflow](/assets/post-images/Socket-Workflow.png)

Java has built-in Server Sockets and Sockets, so accomplishing that in my HTTP server was not that hard, especially with the additional help of input and output streams (the socket in/out data.) To read from it I created these objects:

```java
socket = serverSocket.accept();
output = new DataOutputStream(socket.getOutputStream());
reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
```

To say, get the HTTP request like `GET /foo HTTP/1.1` I read the first line of reader:

```java
reader.readLine();
```

Writing, or displaying some bytes is done through either `output.writeBytes(someBytes)` or `output.write(stuff)`.

It became pretty intuitive after I attained a basic understanding of these processes. It's low-level but that doesn't mean it is confusing or obtuse. I'm kind of getting into it.
