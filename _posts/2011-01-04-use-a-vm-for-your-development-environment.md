---
layout: post
title:  "Use a VM for Your Development Environment"
date:   2011-01-04 21:08:00 -0600
permalink: /2011/01/04/use-a-vm-for-your-development-environment
author: ryin
categories:
- tips
tags:
- lamp
- macbook
- rails
- ruby
- ubuntu
- vm
- vmware
- windows-7
---
For many years, I developed software (mostly [LAMP][lamp] and [Ruby on Rails][rails]) on a MacBook and MacBook Pro. It was always a struggle to have the right stack installed for various projects.  [Mac Ports][ports] became my weapon of choice. Even then, there were enough differences between my development, staging, and production environments to cause unexpected problems. Managing different versions of databases, libraries, etc. was never simple.

At the beginning of 2010, I was fed up with [Steve Job’s reality distortion field][distortion-field] and defected back to the PC camp. Greeting me with open arms was Windows 7, an OS that I continue to praise. However, I longed for my bash prompt and open source stack.

The solution was to run a [VMware][vmware] VM with [Ubuntu][ubuntu] as the guest operating system. This solved many problems.

My development machine became consistent with my staging and production servers.
I can have a different VM for projects requiring different stacks. No more trying to make my laptop a superset of all environments.
When bringing on additional developers to the project, I simply hand them a copy of the VM. Voilà. Their entire development environment is ready to go. No more wasting an entire day on configuring your laptop.
I chose VMware because it is available on Windows, OS X, and Linux and the same VM can run unaltered on all three platforms.
VMware offers snapshots, so you can easily roll back to a known state if you really mess things up.
Now that it’s 2011, a client project requiring OS X has forced me back into Apple’s extortion pricing. This time, however, I will be using the VM solution. I highly recommend it.

[lamp]: http://en.wikipedia.org/wiki/LAMP_(software_bundle)
[rails]: http://rubyonrails.org/
[ports]: http://www.macports.org/
[distortion-field]: http://folklore.org/StoryView.py?story=Reality_Distortion_Field.txt
[vmware]: http://www.vmware.com/
[ubuntu]: http://www.ubuntu.com/
