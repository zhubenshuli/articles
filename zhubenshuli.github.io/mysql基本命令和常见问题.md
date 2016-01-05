title: mysql基本命令和常见问题
date: 2015-07-09 22:23:00
categories: 文档教程
tags: [mysql]
description: mysql基本命令和常见问题...
---

记录自己平常经常使用的mysql基本命令和常见问题...

<!--more-->

## 命令行登录
``mysql -h主机地址 -u用户名 -p用户密码``

## 导入
``source E:/a.sql``

## 清空表
``truncate table mytable``

## 检测字符集问题
``show variables like 'char%'``

## mysql常见问题
* 导入数据提示``MySQL server has gone away``
    在my.ini/my.cnf中修改``max_allowed_pocket``
* 导入数据提示``Unknown command '\n'``
    出现这种错误一般是由于备份数据的字符集和恢复时使用的字符集不一致所致, 命令行登录时: ``mysql -uroot -p --default-character-set=utf8``