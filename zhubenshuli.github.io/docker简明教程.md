title: docker简明教程
date: 2016-08-05 19:37:00
categories: 文档教程
tags: [docker]
description: docker简明教程...
---

记录自己平常经常使用的docker命令...

<!--more-->

## 常用命令
1. 查看正在运行的容器
    `docker ps -a`

2. 镜像构建
    `docker build -t xqd/mysql ./mysql`

3. 容器运行
    * mysql
    `docker run --name xqd-mysql -p 3306:3306 -v /var/projects/data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -it xqd/mysql`
    * nginx
    `docker run --name xqd-nginx -p 80:80 -v /var/projects/data/html:/usr/share/nginx/html -d xqd/nginx`
    * php
    `docker run --name xqd-php -p 9000:9000 -v /var/projects/data/html:/var/www/html -it xqd/php`

4. 进入容器
    `docker exec -it xqd-mysql bash`