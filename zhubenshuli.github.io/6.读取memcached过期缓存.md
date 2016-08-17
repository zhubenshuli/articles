title: 读取memcache过期缓存
date: 2015-04-23 14:29:00
categories: 实战经验
tags: [memcache]
description: 读取memcache过期缓存...
---

今天在线上遇到一个问题:   
读取memcache缓存时，如果缓存过期不存在时，会导致read时间过长，超过将近几百倍的正常读取时间