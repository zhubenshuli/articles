title: php无限极分类
date: 2016-01-08 11:42:00
categories: 实战经验
tags: [php]
description: php无限极分类...
---

在php中巧妙使用**引用**来做无限极分类生成数

<!-- more -->

## 二维数组多字段排序

代码：
```
function generateTree($items){
    $tree = array();
    foreach($items as $item){
        if(isset($items[$item['pid']])){
            $items[$item['pid']]['son'][] = &$items[$item['id']];
        }else{
            $tree[] = &$items[$item['id']];
        }
    }
    return $tree;
}
$items = array(
    1 => array('id' => 1, 'pid' => 0, 'name' => '安徽省'),
    2 => array('id' => 2, 'pid' => 0, 'name' => '浙江省'),
    3 => array('id' => 3, 'pid' => 1, 'name' => '合肥市'),
    4 => array('id' => 4, 'pid' => 3, 'name' => '长丰县'),
    5 => array('id' => 5, 'pid' => 1, 'name' => '安庆市'),
);
print_r(generateTree($items));
```
打印结果：
```
Array
(
    [0] => Array
        (
            [id] => 1
            [pid] => 0
            [name] => 安徽省
            [son] => Array
                (
                    [0] => Array
                        (
                            [id] => 3
                            [pid] => 1
                            [name] => 合肥市
                            [son] => Array
                                (
                                    [0] => Array
                                        (
                                            [id] => 4
                                            [pid] => 3
                                            [name] => 长丰县
                                        )
                                )
                        )
                    [1] => Array
                        (
                            [id] => 5
                            [pid] => 1
                            [name] => 安庆市
                        )
                )
        )
    [1] => Array
        (
            [id] => 2
            [pid] => 0
            [name] => 浙江省
        )

)
```