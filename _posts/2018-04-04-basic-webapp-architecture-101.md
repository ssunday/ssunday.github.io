---
layout: post
title: "Basic Web App Architecture 101"
description: Making a web app...in style
date: 4/4/2018
categories: ["Architecture", "Web App"]
---

Okay, so you want to build a web app.

Let's use a very basic web application for instance.

The user story is this:

1. The user logs in.
2. The user goes to another page, which has a form.
3. When the user clicks submit, data is saved and they can view it later.
4. It will also send an email five minutes later that does something with that data.

That sounds like super simple app? Easy! You can totally build that no problem.

Hold on. Not so fast there.

Let's break it down to see what's actually going on, and then you decide whether it’s truly easy.

**The user logs in.**

This clues us in that there is some form of authentication. There are many forms of authentication, not all created equal or easily created.

Such as:

  - You could use [OAuth](https://en.wikipedia.org/wiki/OAuth), as in, not actually do the authentication yourself. Leave it to Google or whomever to do it for you, and instead store an encrypted oauth token.
  - If you’re using Rails, you could use [Devise](https://github.com/plataformatec/devise) and then it’s not a matter of implementing but rather integrating.
  - Again, if you're using Rails/ActiveRecord, you could leverage [`has_secure_password`](http://api.rubyonrails.org/classes/ActiveModel/SecurePassword/ClassMethods.html#method-i-has_secure_password) to create your own user system while having a streamlined password approach that's been fine-tuned _for_ you.
  - Creating your own authentication system. This is not recommended.

So whatever your choice, your user can log in...granted there is a page, route, and form for them to do that. To even get there, you need one decent skeleton already in place.

Which brings us to:

**The (actual) first step.**

Choosing a framework or lack thereof. You’re going to need to write this web app with *something*. Whether that’s [Ruby on Rails](http://rubyonrails.org/), [Elixir with Phoenix](http://www.phoenixframework.org/), [PHP with Laravel](https://laravel.com/), or something homegrown.

All choices have their pros and cons. Ruby on Rails is battle-tested and has an extremely large community. Elixir with Phoenix is the new cool kid on the block that’s functional, but the newness means that support for everything isn’t there (yet). PHP is the old guard in the web development world, but still very much alive through Wordpress and Laravel.

And then there’s growing your own solution. Which sounds cool and powerful, but realize that there are dozens of things you didn’t realize you had to do because a framework has been doing it for you all along. Things like [cache busting](https://www.keycdn.com/support/what-is-cache-busting/), providing an integrated ORM for easy data access (like Active Record or Eloquent), handling background jobs, and, the most critical part, figuring out how to safely deploy it.

Before I kill your homegrown party completely, let’s go back to this hypothetical web app.

Let’s say you can log in and navigate to another page with a form.

**When the user clicks submit, data is saved and they can view it later.**

Data. Saved. So ergo, a database exists… though what *kind* of database?

Let’s be honest here. We don’t need a fancy NoSQL database for this. A simple, powerful, relational database will suffice.

Which one, though?

If you’re not in the Windows Sphere, you basically have two options:

- [PostgreSQL](https://www.postgresql.org/)
- [MySQL](https://www.mysql.com/)

Both are powerful in their own right. Postgres has more bells and whistles that make it very attractive—such as a JSON data type, and having a boolean type (unlike MySQL which has only tinyint.) MySQL is more popular and has more clattering around it because of its age.

Whatever the choice, there you go, you have a database. And you’ll have to integrate it with your application using some programmatic interface, be it [Active Record](http://guides.rubyonrails.org/active_record_basics.html), [Eloquent](https://laravel.com/docs/5.4/eloquent), or whatever.

All that in place, congrats! You saved data into a database!

The fun doesn’t stop there.

**It will also send an email five minutes later that does something with that data.**

Emailing. Scheduling. Obviously, we don’t want the user to click something and have to wait five minutes for that email to send. So that click needs to schedule and set something to happen in the background.

The most robust way of doing this is have the web app send a message to a queue and have a worker read the message from the queue and do what needs to be done. In more specific terms, you configure Rails through [Active Elastic Job](https://github.com/tawan/active-elastic-job) to send a serialized message to an [AWS SQS](https://aws.amazon.com/sqs/) Queue, and a worker takes the message from the queue and processes at whatever time you scheduled.

Having a queue and a worker provides scalability and doesn’t block the web app or user from doing something else while it waits to do something in the background.

As for the emailing part of it, your options are determined by context, but some choices are:

- [Mailgun](https://www.mailgun.com/)
- Using an email account from Outlook, Gmail, etc.

This is with a complimentary service/tactic for not sending emails out in development. Like logging instead of sending, or using something like [Mailtrap.io](https://mailtrap.io/).

With all that configured, magically no doubt, your web app is done! Either you learned how amazing Rails/Phoenix/Laravel is or how rewarding/painful it is to build your own system. While also learning that a lot goes into building a web app. Maybe more than you thought at first.

But it’s over. Right?

Of course not!

We didn’t cover testing *or* deploying!

All this time and effort choosing technologies and setting up the basic flow of your web app, and it is neither properly maintainable nor an actual web app yet. If you're planning building a web app for whatever reason, do not underestimate the complexity. Overestimate it greatly if you have to as you'll probably be right on the mark. You may think it's simple, list out a few steps and it seems simple, but there are countless other steps and choices within them. There's _always_ something more to do.

As I tend to say now, everything is a work in progress. But this eternal WIP progresses with each phase of development so it's not _completely_ hopeless. A mostly finished product looms on the horizon--you just have to push through to get there.
