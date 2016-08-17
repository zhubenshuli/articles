title: phpredis事务
date: 2015-06-21 09:56:00
categories: 文档教程
tags: [redis]
description: phpredis事务的调用...
---

phpredis事务的调用有两种模式：``Redis::MULTI``和``Redis::PIPILINE``，默认是``Redis::MULTI``模式，相比于默认模式，``Redis::PIPELINE``管道模式速度更快，但没有保证原子性，有可能造成数据的丢失。

<!-- more -->

实例：
```php
$redis = new Redis();
$redis->connect('127.0.0.1', 6379);
$redis->select(25);
$pipe = $redis->multi(Redis::PIPELINE);

$uids = array(1001, 1002, 1003, 1004, 1005);
foreach($uids as $v) {
    $pipe->hGetAll("user:uid:" . $v);
}

$replies = $pipe->exec();
$pipe->discard();

$userinfo = array_combine($uids, $replies);
```

管道执行之后返回的数组是按照命令执行的顺序排列的，可以使用``array_combine``进行数据的组合。