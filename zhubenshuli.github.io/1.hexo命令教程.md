title: hexo命令教程
date: 2014-12-05 10:38:16
categories: 文档教程
tags: [hexo]
description: hexo常用命令...
---

记录自己经常使用到的hexo命令

<!--more-->

## hexo 项目部署到 github 上
```
hexo clean
hexo generate   #生成静态页面至public目录
hexo deploy     #将.deploy目录部署到GitHub
```

## 常用复合命令
```
hexo s -g #生成加预览(本地调试查看)
hexo d -g #生成加部署(上传到服务器)
```

## 简写
```
hexo n == hexo new
hexo g == hexo generate     #生成静态页面至public目录
hexo s == hexo server       #启动本地服务, 进行文章预览调试
hexo d == hexo deploy
```

## 常见问题
1.hexo deploy命令显示ERROR Deployer not found : github  
    deploy的type改成git，然后运行下npm install hexo-deployer-git --save

## jacman文章语法
```
title: postName #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: example #分类
tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 附加一段文章摘要，字数最好在140字以内。
---

以下正文
```