---
layout: post
title:  ".ssh/config file"
date:   2011-01-02 21:51:00 -0600
permalink: /2011/01/02/sshconfig-file
author: ryin
categories:
- configuration
tags:
- config
- scp
- ssh
---
If you use the command line to ``ssh`` or ``scp``, save time by utilizing a ``.ssh/config`` file. This file will save the settings for any particular ``Host``.  While there are a ton of settings, here is a simple example:

    Host dev1
    HostName dev1.mydomain.com
    User deploy
    Port 2222

Entering ``ssh dev1`` is equivalent to ``ssh -p 2222 deploy@dev1.mydomain.com``. Similarly, ``scp sample.file dev1:mytempfolder/`` is equivalent to ``scp -P 2222 sample.file deploy@dev1.mydomain.com:mytempfolder/``. Combining a ``.ssh/config`` file with ``ssh`` public key authentication, you will be able to login and/or copy files to and from remote servers with ease.
