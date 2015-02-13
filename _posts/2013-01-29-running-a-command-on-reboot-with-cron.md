---
layout: post
title:  "Running a command on reboot with cron"
date:   2013-01-19 12:28:00 -0600
permalink: /2013/01/19/running-a-command-on-reboot-with-cron
author: ryin
categories:
- tips
tags:
- cron
- linux
- reboot
---
While investigating the [whenever gem](https://github.com/javan/whenever), which allows you to schedule [cron](http://www.manpagez.com/man/5/crontab/) jobs as part of your Ruby project, I learned something new about cron. You can start a process on reboot with this syntax:

    @reboot /path/to/command

In addition to allowing a non root user to execute commands on startup, the ``@reboot`` option allows you to keep your server deployment dependencies (sphinx, thin, etc.) in a single location. Sweet.
