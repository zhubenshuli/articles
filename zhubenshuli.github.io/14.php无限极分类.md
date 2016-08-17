title: php无限极分类
date: 2016-01-08 11:42:00
categories: 实战经验
tags: [php]
description: php无限极分类...
---

在php中巧妙使用**引用**来做无限极分类生成树，并且使用压栈的方式来遍历

<!-- more -->

## 无限极分类

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
$tree = generateTree($items);
print_r($tree);
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

## 遍历无限极分类数组
```
// 用压栈的方式遍历数组，非递归方法
foreach ( $tree as $k => $v ) {
    
    // 给栈赋予第1条数据
    $list[0] = $v;
    
    // 只要栈$list 不为空，就一直遍历
    while ( !empty( $list ) ) {
        
        // 取出并删除栈顶部的1条数据
        $one = array_shift( $list );
        
        // 打印取出的那条数据
        echo ' name: ' , $one['name'] , ' <br>';

        // 如果取出的那条数据有子节点, 把子节点合并、存入到栈list中去
        if ( isset( $one['son'] ) ) {
            $list = array_merge( $list , $one['son'] );    
        }
    } 
}
```
