title: linux常用命令
date: 2015-05-12 21:45:00
categories: 文档教程
tags: [linux]
description: linux常用...
---

记录自己平常经常使用的linux命令...

<!--more-->

## 系统
1.显示系统运行信息:
```
uptime
```
2.查看磁盘空间信息:
```
df -hl
```
3.查看端口使用情况:
```
netstat -apn
netstap -noap | grep 端口号
```

## 软件
1.移除软件包和配置文件:
```
sudo apt-get purge 软件名
```
2.获取包的相关信息:
```
apt-cache show 包名
```
3.apache错误日志位置:
```
/var/log/apache2/error.log
```

## 用户
1.修改用户密码:
```
sudo passwd 用户名     (用户名为空表示启用root，即修改root密码)
```
2.增加用户:
```
sudo adduser 用户名    (在/home目录下添加一个用户目录)
sudo useradd 用户名    (不会添加用户目录)
```
3.删除用户:
```
sudo userdel 用户名    (参数-r会彻底删除用户相关数据)
```
4.查看所有用户:
```
cat /etc/passed
```

## 文件
1.更改文件所有者:
```
chown -R 用户名 文件或目录;
```
2.更改文件夹/文件名:
```
mv 修改前文件名 修改后文件名;
```
3.更改文件权限
```
chmod 777 文件名
```
4.解压文件
```
tar –xvf file.tar //解压 tar包
tar -xzvf file.tar.gz //解压tar.gz
tar -xjvf file.tar.bz2   //解压 tar.bz2
tar –xZvf file.tar.Z   //解压tar.Z
unrar e file.rar //解压rar
unzip file.zip //解压zip
```
5.查找文件
```
find / -name php.ini
```