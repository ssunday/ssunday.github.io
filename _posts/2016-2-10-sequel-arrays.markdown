---
layout: post
title: Tic Tac Toe Sinatra Sequel
description: Investigating Sequel and getting lost
date: 10/2/2016
---

As iterated in [previous](http://ssunday.github.io/2016/database-datamapper/) [posts](http://ssunday.github.io/2016/datamapper-vs-activerecord/), I am using Datamapper as the go between for my database and Tic Tac Toe Sinatra web app. For the sake of diversity and learning other ways to manage data in databases, I looked into seeing how easy it would be to switch to Sequel as the manager.

At first, it looked easy.

The command functions are, for the most part, all the same name and function as described. Models exist in Sequel, which I had been using in Datamapper. Defining property types of the things of the model/resource to be stored in the database also exists in Sequel as schema that can be defined within the model class, granted you load the schema plugin.

Doings this looks something like this:

```ruby
class Game < Sequel::Model
  plugin :schema
  set_schema do
    primary_key :id
    String :name
    Float :price
    String :player_one_marker
    String :player_two_marker
    String :player_turn
    Boolean :player_one_ai
    Boolean :player_two_ai
    column :game_board, 'Text[]'
    Boolean :active
    String :end_game_state
  end
  create_table unless table_exists?
end
```

I did some other refactoring to integrate the slightly different set up and it all looked well and good until I found the hangup that broke it all apart and made me give up on converting it. It has to do with postgres, which the heroku database I am using uses, and arrays. Mostly arrays.

On the above model, one line in the schema looks different:

```ruby
column :game_board, 'Text[]'
```

Why? Because, unlike datamapper, there isn’t a simple way to specify that the property is an array in Sequel. You have to create a column and specify in quotes what general type of data it is. From what I understand of the documentation, this can be text, varchar, or int.

This threw me for a bit of a spin, then I continued on and switched over what I could, but still nothing was working. The reason why was how postgres stores arrays and how Sequel deals with it. Sequel doesn’t have a particularly native way of handling postgres arrays. A plugin is needed and extensions and all that, to make sure the arrays are being converted as expected.

I have a feeling why this was not the case with Datamapper was that in the configuration for the database, it explicitly stated it was a postgres database, and there were adapters that you had to require and load in before even doing anything.

For data mapper and postgres, in the gemfile, you needed to have these lines to make it all work:

```ruby
gem 'data_mapper'
gem 'dm-postgres-adapter'
gem 'pg'
```

Sequel just needs Sequel, and if you need to do anything you have to specifically ask for it where you needed it and apply the extensions/plugins to make postgres and Sequel work together. It doesn’t communicate or know exactly where the data is going or how it is working together. Things are tweaked for the things that are needed to change, rather than setting it up to all work together for a specific reason.

But in my case, Sequel, its plugins, and the postgres database really weren’t gelling together. Even with all the postgres array plugins and functions, it wasn’t reading the arrays from the database in any coherent manner, contrary to what the (rather gnarly) documentation was explaining would happen. It was not performing as advertised, which is why I eventually gave up on it. Also the staggering lack of support I found on the internet. There was barely any community talk of people using it or describing how it should be used. Which I found irritating and troublesome.

Anyway, the major differences between sequel and Datamapper that I see are how they are structured and set up.

Sequel is more alter-as-you-go, as evidenced by having to tape together compatibility with certain database types with extensions and plugins at the points where it is needed, rather than with Datamapper, where you define what it is you are storing the data in right off the bat and it’ll configure itself to deal with the data as it ought to be. Datamapper is smarter and kinder, but Sequel is probably more flexible and has more advanced utility and customizability. I can’t verify any of this, this is just my feeling from the entire experience in reading about it all.

Speaking of the entire experience, it has been a great learning experience. Even if I didn’t end up really doing anything with Sequel, I gained insight into a how a different tool worked, and how databases can store data. It was also a lesson into documentation and support, or the lack thereof that can exist for a particular system.

The journey is more important than the destination, yada yada.
