---
title: The short story about my OpenSUSE installation
date: 2018-06-11
nopaging: true
noread: true
tags:
 - opensuse
 - linux
 - yast
---

## Installation

I love OpenSUSE, I used it when its version was 9. I remember the beautiful KDE, perfectly working YaST. Or maybe I am just old enough so that all those things seem nice to me.

Long story short after long period of using fedora/ubuntu I decided to find out how good OpenSUSE is. I took my Intel NUC, put the flash drive with dowloaded image in it, and pressed power button.

Pretty boot menu

![Boot menu](/img/opensuse/install-1.jpg)

And you know what, I hadn't put in the network cable before I started. Guess what happened! Installator found wireless module, turned it on, and asked me for an SSID!
The ncurces interface looks a bit oldschool, but who cares, it works! I would also prefer to see the list of existing wireless networks, but it's good enough. Well done!

![Wireless network](/img/opensuse/install-2.jpg)

Then it asked me for a password.

![Wireless password](/img/opensuse/install-3.jpg)

And finaly connected to the network.

![Wireless DHCP](/img/opensuse/install-4.jpg)

Moreover, it figured out that my installation image was a bit outdated. So I let it download the latest one. No additional actions from me, this is how things should be done in 2018.

![Update](/img/opensuse/install-5.jpg)

The other installation is quite boring, because it just works. I won't show you screens, you might see it before. If you didn't, the best way to do it is to try OpenSUSE on your own.

## There is also something to improve

I choose the minimal installation. After I had installed the system I noticed that the network interfaces were down. Well, I tried to start wireless network, I ran YaST in console mode, choose network configuration, and you know what. It said, that wpa_supplicant was not installed. Eventualy I was not able to connect to the wireless network. I got an chicken and egg problem. After all I used a cable and installed all packages that were needed, but you know, it may be improved. Hopefuly it seems easy.

## Resume

I used OpenSUSE long time ago. Although I do not have much experience using the latest relases. However it looks good, it's stable even though this is Tumbleweed (which means, a rolling update distro), zypper works fast, it has all packages that I need. Well, I will give it a shot.