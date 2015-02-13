---
layout: post
title:  "Reloading your development database with a single command"
date:   2011-03-09 10:10:00 -0600
permalink: /2011/03/09/reloading-your-development-database-with-a-single-command
author: ryin
categories:
- database
- tips
tags:
- mysql
- ssh
---
Reloading your development database from a copy on the staging or production server can be done with a single command. With the magic of ssh, key pair authentication, and ``.my.cnf`` files on the server and your development box, you can execute the following:

    ssh -C username@remotehost.com 'mysqldump myapp_staging' | mysql myapp_development

Let’s examine the entire command in pieces. ``ssh`` followed by a command allows you to execute that remote command and have its output sent to the originating server’s ``stdout``. ``mysqldump myapp_staging`` is executed on the remote server and the ``-C`` flag instructs ``ssh`` to compress the data from the remote server. Then, ``mysql`` executes locally to run the sql statements on the ``myapp_development`` database. Voilà, you have reloaded your development database with a copy from the staging server with a single command.
