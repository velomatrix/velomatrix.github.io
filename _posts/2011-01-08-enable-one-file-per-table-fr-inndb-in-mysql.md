---
layout: post
title:  "Enable one file per table for innodb in MySQL"
date:   2011-01-08 00:23:00 -0600
permalink: /2011/01/08/enable-one-file-per-table-for-innodb-in-mysql
author: ryin
categories:
- database
tags:
- disk-storage
- innodb
- mysql
---

I’m not sure why this setting is not enabled by default, but every [MySQL][mysql] installation should have this line in the ``[mysqld]`` section of its ``my.cnf`` file:

    innodb_file_per_table

This setting instructs MySQL to create a separate file for each innodb table’s data. By default, MySQL stores all innodb data (from all databases) in a single file. Now recall that when you delete data from an innodb table, the actual disk storage is not recovered. Instead, MySQL marks the storage region so that when new data is added, that region can be re-used.  That is a sensible strategy, but fails miserably when you need to delete a lot data and recover the corresponding disk storage.

With a single file for all innodb data, recovering disk storage amounts to backing up the database, dropping and re-creating the database, and then reloading the database from the backup.  In the process, you have to stop your server and remove the ``/var/lib/mysql/ibdata1`` file.  This is rarely a viable strategy.  If you are in desperate need to recover disk space on your server, it’s doubtful that you have room to store the database backup. Moreover, the backup and restore process is far from instantaneous when you’re dealing with hundreds of gigabytes of data. This all amounts to a lot of downtime.

Do things right from the start.  Add ``innodb_file_per_table`` to your ``my.cnf`` file.  You will have to restart MySQL for this change to take effect. Now when you want to free up disk space, you can work at the granularity of a single table instead of all databases utilizing innodb.

For example, if you want to clear out the majority of a fictitious table named ``really_big_table``, start by running an ``INSERT SELECT`` statement to store a copy of the data you want to keep into a temporary table. Then ``DROP really_big_table`` and re-``CREATE`` it. Now load the data from the temporary table back into ``really_big_table`` via another ``INSERT SELECT``. Your disk storage has been recovered.

[mysql]: http://www.mysql.com
