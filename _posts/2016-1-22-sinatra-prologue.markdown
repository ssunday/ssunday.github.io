---
title:  "Sinatra: Something Like a Prologue"
description: Beginning steps in understanding Sinatra and Web apps
date: 22/1/2016
---
Web stuff is not really my thing. My understanding of it rests solely with Wordpress, which I am familiar with only as an aggressive user. My knowledge can be classified as a ‘deep puddle.’ What I’m getting is that web apps are like magic to me. Very mystified and illusive to my understanding.

Which is probably why this whole turning the Tic Tac Toe game into a web app was a muddled affair to begin with. Why I even thought I could handle Ruby on Rails is beyond me, but I tried it. Tried being the operative word. If I wrote a blog post on my experiences using rails I would call it ‘Falling Off the Rails.’ But I’m not going to. Instead, I’ll talk about how I moved onto the smaller, easier world of Sinatra.

It was difficult at first, but with the help of [this tutorial series](http://code.tutsplus.com/tutorials/singing-with-sinatra-the-recall-app--net-19128), I was able to grasp the mere basics of it.

The core file of the application boils down to two major parts: ‘get’ and ‘post.’ Get is used for displaying stuff and is what the code does when the browser ‘gets.’ Post is used when the user does something and the code reacts.

For making simple pages, having this works fine:

```ruby
get ‘/‘ do
	“hello world”
end
```

But that isn’t really all that exciting or complex. To do more with the display, one must create a .erb page, which is an embedded Ruby template. Basically HTML with the ability to talk with Ruby. It’s pretty nice.

Example .erb file from my Tic Tac Toe Web App w/ Sinatra:

```html
<!doctype html>
<html lang="en">
<head>
	<title><%= @title %> </title>
</head>
<body>
	<header>
  <% if session["game"].player_one_won? %>
      <h1> Player One has Won! </h1>
  <% elsif session["game"].player_two_won? %>
      <h1> Player Two has Won! </h1>
  <% else %>
      <h1> The Game is Tied! </h1>
  <% end %>
	</header>
  <br>
	<h2> Thanks for playing!</h2> <br>
  <h2> <a href="/settings"> To play again, click here. </a> </h2>
</body>
</html>
```
<% %> brackets are for straight Ruby logic ode, where <%= %> are for displaying some Ruby variable or code. And to display it with the get method of sorts:

```ruby
get '/' do
	erb :index
end
```

At first I was using a ‘haml’ format instead of erb, but haml didn’t have the flexibility I needed, so I switched out for erb.

In theory I can put all the get and post methods into one class and run it from another to make it easier to read. Right now I have all the gets/posts in a organized line in a ‘main.rb’ file. I’m debating whether to change that, as that seems to be a more common trend among Sinatra users. I’ll probably do that once I have everything else squared away in the Tic Tac Toe Web App.

Most of the app is finished, which you can see [here on github,](https://github.com/ssunday/TicTacToeSinatra) but it isn’t pretty and it doesn’t flow that well. The problem with web apps is that web design is a thing and it should, well, look nice and easy to see. This is why Wordpress is amazing—it removes the need to mess around with how things look. But alas, this is not as simple, but it is a far more educational experience. I like it and hate it all at the same time.
