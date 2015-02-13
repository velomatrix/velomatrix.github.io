---
layout: post
title:  "Ubuntu does not reset MOTD after updating"
date:   2011-05-02 08:56:00 -0500
permalink: /2011/05/02/ubuntu-does-not-reset-motd-after-updating
author: ryin
categories:
- tips
tags:
- motd
- ubuntu
- vm
---
After successfully updating my Ubuntu 10.04.02 64-bit VM with the usual:

    sudo apt-get update && sudo apt-get upgrade

The message of the day (MOTD) did not reset the number the number of packages that required updating. Mine was stuck on:

    30 packages can be updated.
    23 updates are security updates.

To remedy this, clear out ``/etc/motd.tail`` with this command:

    cat /dev/null > /etc/motd.tail

When you login again, all will be right with your MOTD.
