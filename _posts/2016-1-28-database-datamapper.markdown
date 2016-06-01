---
layout: post
title: Database, Datamapper, Data Everywhere
description: Deploying the app so others can use it and containing data for use.
date: 28/1/2016
---

Making an app with Sinatra and Ruby is all well and good, but it is limited by the fact that to use it one has to run it locally. Which means they have to download all the files and use the terminal. Way too much work, in my opinion. A way to make it easier for a prospective user to play my trashy tic tac toe game is to deploy it using Heroku. So the entire world can share in playing tic tac toe.

Until this endeavor, I had never really knew what Heroku was. Now I do know. It is where one can deploy their apps onto a website where anyone can access. It’s quite wonderful and easy to connect with a github repository. On the free plan they even give you a free database, which I used.

Before I used Heroku’s Postgres database, I had been using Ruby’s sessions to save information across a game. Sessions worked fine if you were just intending to have the game work in a straight line with clear reset points, but it doesn’t allow you to see past games or resume games. So that’s where a database comes in.

For what method of saving data to the database, Ruby has two major options: Datamapper and Active Record. I chose the earlier because it seemed more flexible and it seemed like a popular option with Sinatra.

With Datamapper, I created a ‘resource’ called Game which would hold all the information. In the class there are properties, basically what is being saved to the database.

```ruby
class Game
  include DataMapper::Resource
  property :id, Serial
  property :player_one_marker, String
  property :player_two_marker, String
  property :player_turn, String
  property :player_one_ai, Boolean
  property :player_two_ai, Boolean
  property :game_board, Object
  property :previous_or_active, String
  property :end_game_state, String, :required => false
end
```
Each property has its own type. :game_board is an Array object, the markers are strings, and so on. Each instance of game, or entry in the database, needs a unique key so one could either use one of the properties as a unique key and set it to the key with the :key => true option or use Datamapper’s ‘natural key’ which is the :id property. There are other options, just as 'required,' one can apply to properties.

Making a new ‘game’ is as simple as declaring a new object. To set the properties…just set whatever properties and then save it.

```ruby
@game = Game.new
@game.previous_or_active = "Active"
...
@game.save
```
And so on. Getting a particular game in the database is easy as well. You can get it by id, match it by property, or get all games of a certain criteria such as here:

```ruby
@unfinished_games = Game.all(:previous_or_active => "Active")
@previous_games = Game.all(:previous_or_active => "Previous")
```

So, in my limited experience, I have found that Datamapper is really flexible and easy to use. There is a lot of community support around it so figuring out a solution to a particular problem was not hard. Setting up the Postgres database was not that hard either, though I did have to reinstall postgres because it was missing some critical files that were needed to set up the Datamapper postgres adapter. Other than that, the documentation was easy to read so setting it all up was breezy and sort of fun.
