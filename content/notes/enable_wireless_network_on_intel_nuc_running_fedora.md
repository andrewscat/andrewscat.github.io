---
title: Enable wireless network on Intel NUC running Fedora Linux
date: 2018-02-07
nopaging: true
noread: true
tags:
 - fedora
 - linux
 - nuc
 - intel
 - wireless
 - wifi
---

I am a happy owner of Inetl NUC computer. Recently I installed Fedora on it (right after [I tested it as a VM](/notes/my_journey_with_fedora/)). It was minimal installation. After I had logged in, I noticed that wireless network interface was unavailable. Quite wierd, taking into account that it worked fine during the installation process.

I looked around, device was connected:
```
# lspci
...
3a:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
...
```

But no wireless interfaces found
```
# modprobe iwlwifi
# ifconfig  -a
eno1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.103  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::3730:ac97:2a6a:55a7  prefixlen 64  scopeid 0x20<link>
        ether f4:4d:30:6d:f9:6e  txqueuelen 1000  (Ethernet)
        RX packets 62642  bytes 90956956 (86.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 27661  bytes 2276244 (2.1 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 16  memory 0xdc300000-dc320000
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

What's in logs: 
```
# dmesg | grep iwlwifi
[    2.935615] iwlwifi 0000:3a:00.0: enabling device (0000 -> 0002)
[    2.942945] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-34.ucode failed with error -2
[    2.942956] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-33.ucode failed with error -2
[    2.942963] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-32.ucode failed with error -2
[    2.942970] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-31.ucode failed with error -2
[    2.942977] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-30.ucode failed with error -2
[    2.942984] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-29.ucode failed with error -2
[    2.942990] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-28.ucode failed with error -2
[    2.942998] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-27.ucode failed with error -2
[    2.943015] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-26.ucode failed with error -2
[    2.943021] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-25.ucode failed with error -2
[    2.943028] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-24.ucode failed with error -2
[    2.943036] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-23.ucode failed with error -2
[    2.943042] iwlwifi 0000:3a:00.0: Direct firmware load for iwlwifi-8265-22.ucode failed with error -2
[    2.943043] iwlwifi 0000:3a:00.0: no suitable firmware found!
[    2.943063] iwlwifi 0000:3a:00.0: minimum version required: iwlwifi-8265-22
[    2.943095] iwlwifi 0000:3a:00.0: maximum version supported: iwlwifi-8265-34
[    2.943111] iwlwifi 0000:3a:00.0: check git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
```

Aha! No firmware! Honestly, I thought, it was going to be installed, since it was working during installation. However no big deal to install in right now

```
# dnf install iwl7260-firmware
```

```
# modprobe -r iwlwifi # remove module
# modprobe iwlwifi
# ifconfig -a
eno1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.103  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::3730:ac97:2a6a:55a7  prefixlen 64  scopeid 0x20<link>
        ether f4:4d:30:6d:f9:6e  txqueuelen 1000  (Ethernet)
        RX packets 68319  bytes 98239380 (93.6 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 30508  bytes 2914398 (2.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 16  memory 0xdc300000-dc320000
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
wlp58s0: flags=4098<BROADCAST,MULTICAST>  mtu 1500
        ether f8:63:3f:37:a3:e3  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Cool! It works! Let's connect to the wireless network with `nmcli`. But first things firgst, make sure that NetworkManager wifi plugin installed

```
# dnf install NetworkManager-wifi
```

Connect to the wifi network
```
# ifconfig wlp58s0 up
# nmcli dev set wlp58s0 managed yes
# nmcli device wifi connect <SSID|BSSID> password <password>
```

I remember the time when configuring wi-fi on Linux was like a chalange. You never know what you'll face and I could hardly get it work. But things are changing, currently make Linux work with wireless network seems like a walk in the park with your dog. I like seeing how this world is changing and it is definitely going in right direction.