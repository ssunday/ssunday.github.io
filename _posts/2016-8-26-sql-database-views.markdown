---
layout: post
title: Database Views
description: Fake tables to see stuff
date: 26/8/2016
category: "SQL"
---

Database views are a type of stored query that create a pseudo-'table'. Instead of doing the same join table mish-mash to get the relationship of data needed, you can create a view that will store the query to get that data. This query is run every time so the data is dynamic and not static. It will get the exact data needed at time of execution, not what was present at view creation.

Why this is kind of cool/practical:

* Mild performance increase.

* Easier to understand than a crazy query.

* Logic is hidden. Can be used for security reason.

* It is 'virtual'---requires little space.

* Allows creating a tiered database structure of lower level, more hidden tables and more upper level tables that are accessed more freely.

Views can be created by doing `CREATE VIEW [View Name] AS [Query you want as the view]` and then to get the data just use `SELECT * FROM [View Name].` (Brackets can be ignored.) Dropping it is like dropping a table. `DROP VIEW [View Name]`.

I like to think of views as quasi-classes/functions. Like prepared statements, but used more for visualization of data rather than as a calculation. Something that needs to be dynamic and easily accessed. Which is pretty awesome. I haven't found a use for them yet, but it seems like the capability of views can really extend the power of one's database. One day they will be tremendously useful.
