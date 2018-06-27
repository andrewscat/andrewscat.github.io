---
title: Create VM in QEMU/KVM environment
date: 2018-03-03
nopaging: true
noread: true
tags:
 - kvm
 - qemu
 - vm
---

Here I am going to create a VM. Since I've never tried CentOS 5, I decided to give it a shot. It has the old good sysv init system, it's old, not obsolete. By this examle I will show you how to create and manage QEMU/KVM virtual machine without GUI utilities.
First of all create a virtual disk of the desired size. Here for example, we will create a 20 GB disk with the raw disk format:
You can also try to use qcow2 format which gives you some additional benefits.
```bash
qemu-img create -f raw -o size=10G /media/tb/qemu/centos5.img
```

Then start virt-install by running the following command: 
```bash
virt-install \
  --name Centos5 \
  --ram 1024 \
  --disk path=/media/tb/qemu/centos5.img \
  --vcpus 1 \
  --os-type linux \
  --os-variant rhel5 \
  --network bridge=virbr0 \
  --graphics vnc,port=5999,listen=0.0.0.0 \
  --console pty,target_type=serial \
  --cdrom /media/tb/iso/CentOS-5.11-x86_64-netinstall.iso
```

Meaning of options are quite clear. By the way, you can check the list of OS variants with
```bash
virt-install --os-variant list
```

Check if the VM is up
```bash
virsh list --all
```

If you don't see your VMs, try to add connection line
```bash
virsh -c qemu:///system list
```
or to make it permanent, uncomment the line in /etc/libvirt/libvirt.conf
```bash
uri_default = "qemu:///system"
```

Once the VM is running, you can connect to it via VNC and continue installation. I used VNC Viever for Mac OS. Pay attention, that VNC port was set to 5999.

![VNC connect](/img/qemu_kvm_centos/centos-1.png)

Let the installation begin.

![CentOS 5 installation](/img/qemu_kvm_centos/centos-2.png)

## Configure CentOS 5 repo

Since CentOS 5 is not supported anymore, I replaced the preconfigured repo with:
```ini
# cat /etc/yum.repos.d/CentOS-Vault.repo
[C5.11-base]
name=CentOS-5.11 - Base
baseurl=http://vault.centos.org/5.11/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

[C5.11-updates]
name=CentOS-5.11 - Updates
baseurl=http://vault.centos.org/5.11/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

[C5.11-extras]
name=CentOS-5.11 - Extras
baseurl=http://vault.centos.org/5.11/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

[C5.11-centosplus]
name=CentOS-5.11 - Plus
baseurl=http://vault.centos.org/5.11/centosplus/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
```

As a result I got my CentOS 5 machine. To be honest, I removed it after a couple of hours playing around. It is mostly useles in modern world, but that was worth it.