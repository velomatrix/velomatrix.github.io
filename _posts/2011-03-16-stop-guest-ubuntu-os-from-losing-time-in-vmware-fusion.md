---
layout: post
title:  "Stop guest Ubuntu OS from losing time in VMWare Fusion"
date:   2011-03-16 11:39:00 -0600
permalink: /2011/03/16/stop-guest-ubuntu-os-from-losing-time-in-vmware-fusion
author: ryin
categories:
- annoyances
- vm
tags:
- os-x
- vmware
---
On my MacBook Air, the Ubuntu 10.04 VMWare guest OS was losing time whenever the Air went to sleep. To keep time synchronized between the host and guest, install VMWare Tools AND enable time synchronization by executing sudo ``/usr/bin/vmware-toolbox``. Make sure the following checkbox is selected.

![VMware properties](/assets/vmware-tools-properties.png )
