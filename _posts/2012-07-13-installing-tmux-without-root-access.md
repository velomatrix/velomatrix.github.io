---
layout: post
title:  "Installing tmux without root access"
date:   2012-07-13 01:28:00 -0500
permalink: /2012/07/13/installing-tmux-without-root-access
author: ryin
categories:
- tips
- tools
tags:
- tmux
- root
---
[tmux](http://tmux.sourceforge.net/) is one of the first packages I install on a server. It offers all the advantages of [screen](http://www.gnu.org/software/screen/) and adds in scripting, multiple panes, and other goodies.

However, sometimes you don’t have root access on a server and/or can’t upgrade tmux’s dependencies ([libevent](http://libevent.org/) and [ncurses](http://www.gnu.org/software/ncurses/). In these cases, you can install tmux locally. After many false starts, I was able to get it all working. Hopefully, the gist below will save someone the time and aggravation I went through. A special thanks to this [forum post](http://www.linuxquestions.org/questions/linux-software-2/installing-tmux-from-source-as-non-root-user-857098/) for getting me 90% of the way there.

<script src="https://gist.github.com/ryin/3106801.js"></script>
