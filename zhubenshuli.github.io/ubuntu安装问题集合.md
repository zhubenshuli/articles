title: linux安装问题集合
date: 2016-01-03 19:32:00
categories: 文档教程
tags: [linux]
description: linux安装问题集合...
---

记录自己平常安装linux时遇到的各种问题...

<!--more-->

## detect and nount cd-rom
mkdir /usb
mount -t vfat /dev/sdb1 /usb
mkdir /cdrom
mount -t iso9660 -o loop /usb/isos/xx.iso /cdrom