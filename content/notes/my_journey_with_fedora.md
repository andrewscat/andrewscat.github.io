---
title: My journey with Fedora. The begining.
date: 2018-02-03
nopaging: true
noread: true
---

Let me start with saying that I have been an ubuntu guy. Back in 2008 I met ubuntu first time, since than I have used different linux operating systems. In 2014 I switched to deb-based distros on my desktop. For some reason every time I tried redhat-like OS, the venture failed. Every time some crap happened. In addition, I don’t really like neither the current fedora artwork nor its fonts. Speaking of fonts, ubuntu has the perfect fonts, I loved them. Eventually I got used to ubuntu and its simplicity. But things are changing, and recently I switched to Mac. Although addiction to linux was so strong that I decided to install linux inside VirtualBox on my Mac and use it from time to time. So I was looking for the linux distro for this purpose, and it looked like a time for trying something new. And I’m going to give fedora a shot.

## Part 1. Download and install

I started on getfedora.com, there are three options: server, workstation, and atomic. I want a tiny virtual machine without GUI, so I was in some doubt about which one to choose. After a short meditation I picked workstation one. 
I noticed there was an utility “Fedora Media Write for Mac OS X”, I downloaded it as well. It turned out a java application, that didn’t work. Probably because of some security limitations, I don’t know, I didn’t troubleshoot.

![Fedora media writer](/img/my_journey_with_fedora/fedora_media_writer.png)

Long story short, installing fedora didn’t take a lot of time. Easy peasy, nothing unusual. In a couple of minutes I got fedora installed. What I didn’t like about anaconda, the fedora installer, is that it didn't have text-based mode. I had used it before but I didn’t find a way to use it now. 

Update: I checked and it turned out, it’s still there. But it’s much less usable than debian installer. However, one use installer only once, when the system is being installed, so I can deal with the that.

>Thing to do: try kickstart installer, it looks like an interesting thing.

## Part 2. Configuring.

Once installation was done, I took a snapshot. At this point I wished I had an ansible playbook for startup configuration. Actually I used to have it, but it wasn’t saved. Such a pity, it would came in handy.

![Fedora installed](/img/my_journey_with_fedora/fedora_installed.png)

## Part 3. Configuring

Packages that I installed

- net-tools (I am used to ifconfig)
- micro (I decided to try something but vim)
- pciutils (I was surprised that it wasn't here)
