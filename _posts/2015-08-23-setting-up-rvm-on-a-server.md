---
layout: post
title: "Setting up RVM on a Server"
date: 2015-08-23 06:00:00 -0600
permalink: /2015/08/23/setting-up-rvm-on-a-server
author: nola
categories:
- tips
tags:
- rvm
- setup
---

RVM is a tool to manage ruby versions. You probably have used it in development on your laptop. But how do you set it up on the server to run in a production or staging environment?

I was recently faced with this delima (chef was installed which needed 1.9.3 whereas our sinatra app needed 2.2.0). Someone had used chef to install rvm but it wasn't working. Not being the chef/devops pro I didn't really understand what was needed. I quickly did what I knew how to get it working and it was all a blur (yet I didn't understand enough to update the chef recipe).

Stepping back I installed a virtual machine with the same version of OS that we used and determined to figure out the right way to install it before doing anything with chef. Here's what I did:

After talking to a friend that uses rvm on his server he said to use the multi-user install instructions.

Install rvm for multi-user like this:

```
\curl -sSL https://get.rvm.io | sudo bash -s stable
```

You have to use sudo this `one time only`. No `rvmsudo` ever on this server.

The script created the group `rvm` and all the setup for rvm.

Now add all users that can add versions and gemsets to that group:

Now all `rvm` users can add and change ruby versions as needed:

    [vagrant@localhost mine] rvm install 2.2.0
    [vagrant@localhost mine] rvm install 1.9.3
    
    [vagrant@localhost mine] rvm 1.9.3
    
    [vagrant@localhost mine]$ ruby -v
    ruby 1.9.3p551 (2014-11-13 revision 48407) [x86_64-linux]
    
    [vagrant@localhost mine]$ which ruby
    /usr/local/rvm/rubies/ruby-1.9.3-p551/bin/ruby
    
    [vagrant@localhost mine]$ rvm 2.2.0
    
    [vagrant@localhost mine]$ which ruby
    /usr/local/rvm/rubies/ruby-2.2.0/bin/ruby

Maybe all this is obvious from reading the docs at [rvm.io](http://www.rvm.io) but I missed the key step of adding users to the `rvm` group and understanding the different methods of installing rvm.

I still have to go back and see where the chef script went wrong that my Ops guy used. :)

Hope it saves you some moments (hours?) of frustration. :)
