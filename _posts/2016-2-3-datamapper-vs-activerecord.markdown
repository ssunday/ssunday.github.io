---
title: Datamapper vs ActiveRecord
description: Looking at two database solutions in Ruby. Compare and contrast.
date: 3/2/2016
---

Ruby has two major players in the world of dealing with databases. These two are Datamapper and ActiveRecord. ActiveRecord is popular in the world of Rails, and Datamapper is the option of choice in the wonderland of Sinatra, from my general understanding.

With Datamapper, everything is pretty self-contained within the code. There is really nothing to run on the command line with it—it all happens inside the Ruby files. Configuration is very easy.

Setting up Datamapper with the specific database happens in a single line. To migrate the database, add this line after it:

```ruby
DataMapper.auto_migrate!
```

This sets up the database and tables for the data and clears it for use. This should only be run sparingly, as it clears the information every time the file it is contained in is run. To update the tabels and not lose information, use auto_upgrade, like this:

```ruby
DataMapper.auto_upgrade!
```

This allows the database to be updated and filled with new information and setup.

Both of these methods are much more simplistic than Active Record, which involves creating migrations specifically for each type of model and such. Datamapper handles it all without the coder needing to specify anything. It's really quite nice and easy.

Although in that regard they are different, there are a variety of similar points between them.

To add a new entry, simply create an new object of the specific model, which is defined in its own file/ class:

```ruby
game = Game.new
```

And then set the properties of it to whatever and then save it. Both have it automatically be added and modified into the database.

Getting the data from the specified database is also very similar.

With Datamapper, one can get all of a certain model by doing model_name.all (same as ActiveRecord), or if you want all entries with a certain property, you can specify the value of that property with .all as well. For single instances, .get works the same way.

Some examples of this below:

```ruby
single_game = Game.get(:game_id => 1)
all_games = Game.all
all_active_games = Game.all(:active => true)
```

Active Record is very similar, just with different function names and syntax-style. The function is the same.

```ruby
game = Game.find_by(active: true)
all_games = Game.all
```

There are other little nuances with the basics, but they have the same general toolset and capabilities.

From what I’ve been reading about the two, Active Record has more power to it, but Datamapper is seemingly easier to use and integrate into light-weight apps. That is what I’m getting from the two. There  are probably very good reasons for using one or the other, depending on the context. That is usually the case. People don’t make the same thing twice if there is not a difference that effects usability and execution. There has to be something differentiating the two that makes one more advantageous than the other in a context.

For my Tic Tac Toe app with Sinatra, Datamapper seemed to be the best solution and it has been working out very well.
