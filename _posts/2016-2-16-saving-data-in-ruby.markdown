---
layout: post
title: Saving Data in Ruby
description: Writing data to a CSV file
date: 16/2/2016
---

For my new Ruby project, I am basically creating a app for employees to log their time worked for a particular project type and client. The main component of this app is making so the data is persistent—that it is saved to a file so it can be accessed across multiple sessions of the app. Also so that one can get reports of all the data entered.

There are many different ways of saving data to a file in Ruby. The two I looked at were .txt and .csv. By looked at, I merely researched the general syntax and input/output conventions of each. CSV, being table-and-row based, fit in nicely with the specifications of having each row hold a set of related data, and it parsed out easily, so I chose it.

With writing to a CSV file, the general convention is not to actually store a CSV file object in a variable, but to open it at time of writing and iterate over it as needed.

Such as like this:

```ruby
CSV.open(@time_log_file_name, "ab") do |csv|
      csv << [username, date, hours, timecode, client]
end
```

At the closing of the iteration, the file is closed. The data is inputed into the file as an array, and each array creates a new row with the values inside of it placed in separate columns. It looks like this in a editor like Numbers or Excel:

![TableExample](/assets/post-images/TableExample.png)

Now, to get the data out of the file is as simple as calling:

```ruby
CSV.read(@time_log_file_name)
```

Which returns the information as a nested array, with the rows as the internal arrays. Simple.

There are different read/write/append modes for opening a file that are designated by the typical ‘w,’ ‘r,’ and ‘ab,’ in Ruby’s case, for writing, reading, and appending.

Using a CSV is a really streamlined process and the data is retrieved easily, as it is in array form. And the file format readability is excellent, so if I need to see if something is saving the right way, I can just open up the file and look at it.

I’m a fan of spreadsheets, so picking CSV was pretty obvious choice for me, especially in this context.
