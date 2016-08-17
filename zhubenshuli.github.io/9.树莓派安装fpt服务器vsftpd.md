title: 树莓派安装ftp服务器vsftpd
date: 2015-05-13 22:32:00
categories: 文档教程
tags: [linux, 树莓派]
description: 树莓派安装ftp服务器vsftpd...
---

今天闲来无事就在自己的树莓派上安装了ftp服务器vsftpd，发现安装的过程中还是有很多坑的，特此记录一下：

<!--more-->

1. ``sudo apt-get install vsftpd``

2. ``sudo useradd -d /var/www -s /sbin/nologin ftpwwwer``
``-d``参数设定它的初始登入目录为``/var/www``，``-s``参数设定它不需要登陆系统``/sbin/nologin``，用户名为``ftpwwwer``。
``sudo passwd ftpwwwer``修改密码

3. 配置文件修改  
``sudo vim /etc/vsftpd.conf``
```
禁止匿名用户登录: anonymous_enable=NO
允许本地用户登录: local_enable=YES
用户可写权限: write_enable=YES
支持断点续传: local_umask=022
阻止用户访问上级目录: chroot_list_enable=YES, chroot_list_file的注释去掉
```

4. 建立``/etc/vsftpd.chroot_list``文件，在其中添加用户``ftpwwwer``，多用户注意一行一个。

5. 重启fpt服务器
	``sudo /etc/init.d/vsftpd restart``

6. ``ftp``客户端连接时
* 出现``530 Login incorrect``错误
在保证用户名密码正确时，修改``/etc/vsftpd.conf``
```
pam_service_name=ftp
```
* 出现``500 OOPS: vsftpd: refusing to run with writable root inside chroot()``错误
保证``ftp``根目录不可写即可，比如本例中设置``/var/www``的权限为``r-w``即可