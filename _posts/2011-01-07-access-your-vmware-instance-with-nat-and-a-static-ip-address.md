---
layout: post
title:  "Access your VMware instance with NAT and a static IP address"
date:   2011-01-07 01:08:00 -0600
permalink: /2011/01/07/access-your-vmware-instance-with-nat-and-a-static-ip-address
author: ryin
categories:
- tools
- vm
tags:
- apache
- mysql
- networking
- os-x
- phusion-passenger
- ruby-enterprise-edition
- ruby-on-rails
- ubuntu
- vm
- vmware
- windows
---

Once you have your development environment setup as a VMware VM, you will want to access it with applications running on your host OS.  For example, you want to test your new shiny Ruby on Rails web application (running in your VM) with Internet Explorer on Windows or Safari on OS X

There are three ways to configure the network connection for your VM:

* host-only
* bridged
* [NAT][nat]

Host-only is not interesting for web applications that interact with APIs and services on the internet.

With a bridged connection and [DHCP][dhcp], your VM will have a different IP address as you go from home to office to coffee shop.  It becomes annoying to open a terminal in your VM, run ``/sbin/ifconfig``, copy the IP address, and then go back to the host OS and adjust your hosts file accordingly.  Do this a few times and you will clamor for a better way.

Enter NAT and a static IP address for your VM.  You will have a consistent IP address no matter which network your host is on. Enter this IP address into your hosts file once and you’re done.  Let’s walk through a real life example.

You have 3 in-progress client projects.  You have configured your development VM with the same stack that’s powering your staging and production servers.   In this example, you have a Ruby on Rails application running apache, Ruby Enterprise Edition, Phusion Passenger, and MySQL.  You configure each project with  its own VirtualHost : project1.dev, project2.dev, and project3.dev.  On your host OS, you have a ``host`` file entry like this:

`192.168.154.100 project1.dev project2.dev project3.dev`

Now whether you’re at home, at the office, or sipping some chai tea at a coffee shop, you can access your client projects the same way from a browser on the host OS: http://project1.dev, http://project2.dev, and http://project3.dev.

This seems simple enough, but it turns out that defining a static IP address in your guest Ubuntu VM and having that IP address accessible from the host is not trivial.  Start by running ``ipconfig`` (Windows) or ``ifconfig`` (OS X) on the host OS and look for the IPv4 Address for the VMnet8 adapter.  On my Windows machine, that address is 192.168.154.1.  On my OS X machine, that address is 172.16.252.1.

Now in your Ubuntu VM, configure it to use a static IP address.  This example uses 192.168.154 for the first three octets.  Substitute the first 3 octet values corresponding to your VMnet8 adapter.  In Ubuntu, System -> Preferences -> Network Connections.  On the Wired tab, select the network adapter (usually Auto eth1) and click on Edit.  Select the IPv4 Settings tab and enter/select these values:

* Method: Manual
* IP address: 192.168.154.100
* Netmask: 255.255.255.0
* Gateway: 192.168.154.2
* DNS Servers: 192.168.154.2

192.168.154.100 was chosen for the IP address because 100 is a) easy to remember and b) far enough away from the reserved low single digits to avoid conflicts.  The gateway value was the tricky one.  Most references instruct you to use the IP address, but substitute 1 for the final octet.  However, that IP address was already being used on the host for the VMnet8 adapter.  After much trial and error, it turned out that 192.168.154.2 was the ticket.  The DNS Servers value is the same as the Gateway value.  This instructs the VM to use the host machine to make DNS requests.  Whatever your host machine uses to do DNS lookups, your VM will also use.

After making the settings, restart your networking with ``/etc/init.d/networking restart``.

[nat]: http://en.wikipedia.org/wiki/Network_address_translation
[dhcp]: http://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol 
