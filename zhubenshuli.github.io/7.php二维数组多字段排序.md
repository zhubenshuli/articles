title: php二维数组多字段排序
date: 2015-05-11 19:43:00
categories: 实战经验
tags: [php]
description: php二维数组多字段排序...
---

php中有很多排序函数，下面是比较常见的几种：
* sort() 函数用于对数组单元从低到高进行排序。
* rsort() 函数用于对数组单元从高到低进行排序。
* asort() 函数用于对数组单元从低到高进行排序并保持索引关系。
* arsort() 函数用于对数组单元从高到低进行排序并保持索引关系。
* usort() 使用用户自定义的比较函数对数组中的值进行排序
* uasort() 使用用户自定义的比较函数对数组中的值进行排序并保持索引关联

<!-- more -->

## 二维数组多字段排序
有如下一个数组：
```php
$array_sorted = array(
    array('id' => 2, 'num' => 4, 'coin' => 5000),
    array('id' => 4, 'num' => 3, 'coin' => 6000),
    array('id' => 2, 'num' => 3, 'coin' => 7000),
    array('id' => 2, 'num' => 4, 'coin' => 8000),
    array('id' => 2, 'num' => 4, 'coin' => 7000)
);
```
需要先对``id``升序排列，``id``相同的情况下对``num``降序排列，``num``相同的情况对``coin``升序排列。

比较简单的解决方法就是用``usort()``函数了，代码如下：
```php
usort($array_sorted, function($a, $b){
    $key_orders = array(
        'id'    => 'asc',
        'num'   => 'desc',
        'coin'  => 'asc'
    );

    foreach($key_orders as $key => $order) {
        if($a[$key] == $b[$key]) {
            continue;
        }
        return (($order == 'asc') ? 1 : -1) * (($a[$key] < $b[$key]) ? -1 : 1);
    }

    return 0;
});
```

排序后的结果：
```php
Array
(
    [0] => Array
        (
            [id] => 2
            [num] => 4
            [coin] => 5000
        )

    [1] => Array
        (
            [id] => 2
            [num] => 4
            [coin] => 7000
        )

    [2] => Array
        (
            [id] => 2
            [num] => 4
            [coin] => 8000
        )

    [3] => Array
        (
            [id] => 2
            [num] => 3
            [coin] => 7000
        )

    [4] => Array
        (
            [id] => 4
            [num] => 3
            [coin] => 6000
        )

)
```
