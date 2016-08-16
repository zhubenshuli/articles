title: git简明教程
date: 2016-04-05 13:27:00
categories: 文档教程
tags: [git]
description: git简明教程...
---

记录自己平常经常使用的git命令等...

<!--more-->

## 用户配置
```
git config --global user.name "xuqingdi"
git config --global user.email zhubenshuli@gmail.com
```

```
git config --global core.ignorecase false   // 大小写敏感
git config --global core.autocrlf false     // 不做 lf crlf 转换：
git config --global core.safecrlf true      // 在提交时检查发现混用 lf crlf 则拒绝提交
```

## 常用命令
1. 初始化或者克隆
    `git init`
    `git clone url`

2. 切换分支
    `git checkout branch_name`
    `git checkout -b branch_name` 创建分支并切换

3. 删除分支
    本地: `git branch -D [分支名]`
    远程: `git push [远程名] :[分支名]`

4. 提交
    `git add file_name(*)(.)`
    `git commit -m '备注内容'`
    `git push`
    `git push -u origin branch_name(第一次)`

5. 自己分支为xqd, 合并dev中的内容
    `git checkout xqd`
    `git merge dev`

6. 撤销更改
    命令`git checkout -- readme.txt`意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
        一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态。
        一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

7. 建立本地分支和远程分支关联
    `git branch --set-upstream branch-name origin/branch-name`

6. 暂存相关操作
    `git stash`
    `git stash list`
    `git stash pop`
    `git stash apply ~ / git stash drop ~`

7. 修改仓库地址
    `git remote remove origin`
    `git remote add origin ssh://...`

## 备注
1.ssh 每次push/pull需要输入密码
    将自己的私钥文件取消密码（软件：puttygen）
