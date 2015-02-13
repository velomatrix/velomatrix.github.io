---
layout: post
title:  "Querying large tables"
date:   2011-01-04 21:50:00 -0600
permalink: /2011/01/04/querying-large-tables
author: ryin
categories:
- database
tags:
- optimization
- partitioning
- postgres
- sql
---
I recently completed an optimization pass for a website that does reporting for its clients. A number of reports took more than 30 seconds to compute. As the data grew, performance continued to degrade. The main table in question consisted of tens of millions of rows.

Here was the strategy I employed:

1. De-normalize the data
2. Partition the tables
3. Optimize the indexes on the table
4. Optimize the queries

Step 1 is to avoid joins. Joins are expensive operations. If you can put all the necessary fields in a single table, your queries will also be much simpler and the database won’t have to perform complex operations. Of course, nothing comes for fee. The cost is duplication of data. While space will rarely be your limiting factor, it’s important to take steps to avoid data inconsistencies.

Step 2 serves to divide your large table into smaller ones. One huge advantage is that the indexes for any of the smaller tables will be much smaller. If a table’s index can be loaded entirely into memory, you will notice huge speed improvements. For this particular application, the database is [Postgres](http://www.postgresql.org/) and I was able to utilize the [inheritance](http://www.postgresql.org/docs/current/interactive/ddl-inherit.html) feature to implement [partitioning](http://www.postgresql.org/docs/current/static/ddl-partitioning.html).

Steps 3 and 4 really go hand-in-hand. In an existing application, you have the luxury of examining the slow query logs to determine which queries to focus on. On Postgres, I recommend using pgFouine. As optimization is a never-ending pursuit, these two steps can take as little or as much time as you have. Set realistic goals for your optimization efforts. With Postgres, the [explain analyze](http://www.postgresql.org/docs/current/static/sql-explain.html) command will yield vast amounts of data about your queries and the indexes. Use them often.

This optimization effort allows reports that took in excess of 30 seconds to now return in under a second.
