---
title: Create VM in QEMU/KVM environment
date: 2018-03-03
nopaging: true
noread: true
---

Create a virtual disk of the desired size. Here for example, we will create a 20 GB disk with the raw disk format:
You can also try to use qcow2 format which gives you some additional benefits.
```
qemu-img create -f raw -o size=10G /media/tb/qemu/centos5.img
```

Then start virt-install by running the following command: 
```
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

You can check the list of OS variants with
```
virt-install --os-variant list
```

If you don't see your VMs, try to add connection line
```
virsh -c qemu:///system list
```
or to make it permanent, uncomment the line in /etc/libvirt/libvirt.conf
```
uri_default = "qemu:///system"
```

Since CentOS 5 is not supported anymore, I replaced the preconfigured repo with:
```
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
