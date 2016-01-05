title: crontab 定时任务
date: 2015-06-20 13:37:00
categories: 文档教程
tags: [linux]
description: 通过``crontab``命令，我们可以在固定的间隔时间执行指定的系统指令或``shell script``脚本。时间间隔的单位可以是分钟、小时、日、月、周及以上的任意组合。这个命令非常适合周期性的日志分析或数据备份等工作。
---

通过``crontab``命令，我们可以在固定的间隔时间执行指定的系统指令或``shell script``脚本。时间间隔的单位可以是分钟、小时、日、月、周及以上的任意组合。这个命令非常适合周期性的日志分析或数据备份等工作。

<!--more-->

*<转载地址 <http://linuxtools-rst.readthedocs.org/zh_CN/latest/tool/crontab.html>>*

## 命令格式
```
crontab [-u user] [ -e | -l | -r ]
```

## 命令参数
* ``-u user``：用来设定某个用户的``crontab``服务；
* ``file``：``file``是命令文件的名字,表示将``file``做为``crontab``的任务列表文件并载入``crontab``。如果在命令行中没有指定这个文件，``crontab``命令将接受标准输入（键盘）上键入的命令，并将它们载入``crontab``。
* ``-e``：编辑某个用户的``crontab``文件内容。如果不指定用户，则表示编辑当前用户的``crontab``文件。
* ``-l``：显示某个用户的``crontab``文件内容，如果不指定用户，则表示显示当前用户的``crontab``文件内容。
* ``-r``：从``/var/spool/cron``目录中删除某个用户的``crontab``文件，如果不指定用户，则默认删除当前用户的``crontab``文件。
* ``-i``：在删除用户的``crontab``文件时给确认提示。

## crontab的文件格式
分 时 日 月 星期 要运行的命令

* 第1列分钟1～59
* 第2列小时1～23（0表示子夜）
* 第3列日1～31
* 第4列月1～12
* 第5列星期0～6（0表示星期天）
* 第6列要运行的命令

## 常用方法
### 创建一个新的``crontab``文件
向``cron``进程提交一个``crontab``文件之前，首先要设置环境变量``EDITOR``。``cron``进程根据它来确定使用哪个编辑器编辑``crontab``文件。99%的``UNIX``和``LINUX``用户都使用``vi``，如果你也是这样，那么你就编辑``$HOME``目录下的``.profile``文件，在其中加入这样一行:
```
EDITOR=vi; export EDITOR
```
然后保存并退出。不妨创建一个名为``<user> cron``的文件，其中``<user>``是用户名，例如, ``davecron``。在该文件中加入如下的内容。
```
# (put your own initials here)echo the date to the console every
# 15minutes between 6pm and 6am
0,15,30,45 18-06 * * * /bin/echo 'date' > /dev/console
```
保存并退出。注意前面5个域用空格分隔。

在上面的例子中，系统将每隔15分钟向控制台输出一次当前时间。如果系统崩溃或挂起，从最后所显示的时间就可以一眼看出系统是什么时间停止工作的。在有些系统中，用tty1来表示控制台，可以根据实际情况对上面的例子进行相应的修改。为了提交你刚刚创建的``crontab``文件，可以把这个新创建的文件作为``cron``命令的参数:
```
$ crontab davecron
```
现在该文件已经提交给``cron``进程，它将每隔1 5分钟运行一次。同时，新创建文件的一个副本已经被放在``/var/spool/cron``目录中，文件名就是用户名(即dave)。

### 列出crontab文件
使用-l参数列出crontab文件:
```
$ crontab -l
0,15,30,45,18-06 * * * /bin/echo `date` > dev/tty1
```
可以使用这种方法在``$HOME``目录中对``crontab``文件做一备份:
```
$ crontab -l > $HOME/mycron
```
这样，一旦不小心误删了``crontab``文件，可以用上一节所讲述的方法迅速恢复。

### 编辑crontab文件
如果希望添加、删除或编辑``crontab``文件中的条目，而``EDITOR``环境变量又设置为``vi``，那么就可以用``vi``来编辑``crontab``文件:
```
$ crontab -e
```
可以像使用vi编辑其他任何文件那样修改``crontab``文件并退出。如果修改了某些条目或添加了新的条目，那么在保存该文件时， cron会对其进行必要的完整性检查。如果其中的某个域出现了超出允许范围的值，它会提示你。 我们在编辑``crontab``文件时，没准会加入新的条目。例如，加入下面的一条：
```
# DT:delete core files,at 3.30am on 1,7,14,21,26,26 days of each month
30 3 1,7,14,21,26 * * /bin/find -name 'core' -exec rm {} \;
```
保存并退出。

注解
最好在crontab文件的每一个条目之上加入一条注释，这样就可以知道它的功能、运行时间，更为重要的是，知道这是哪位用户的定时作业。

### 删除crontab文件
```
$crontab -r
```

## 使用实例
**实例1：每1分钟执行一次myCommand**
```
* * * * * myCommand
```
**实例2：每小时的第3和第15分钟执行**
```
3,15 * * * * myCommand
```
**实例3：在上午8点到11点的第3和第15分钟执行**
```
3,15 8-11 * * * myCommand
```
**实例4：每隔两天的上午8点到11点的第3和第15分钟执行**
```
3,15 8-11 */2  *  * myCommand
```
**实例5：每周一上午8点到11点的第3和第15分钟执行**
```
3,15 8-11 * * 1 myCommand
```
**实例6：每晚的21:30重启smb**
```
30 21 * * * /etc/init.d/smb restart
```
**实例7：每月1、10、22日的4 : 45重启smb**
```
45 4 1,10,22 * * /etc/init.d/smb restart
```
**实例8：每周六、周日的1 : 10重启smb**
```
10 1 * * 6,0 /etc/init.d/smb restart
```
**实例9：每天18 : 00至23 : 00之间每隔30分钟重启smb**
```
0,30 18-23 * * * /etc/init.d/smb restart
```
**实例10：每星期六的晚上11 : 00 pm重启smb**
```
0 23 * * 6 /etc/init.d/smb restart
```
**实例11：每一小时重启smb**
```
* */1 * * * /etc/init.d/smb restart
```
**实例12：晚上11点到早上7点之间，每隔一小时重启smb**
```
* 23-7/1 * * * /etc/init.d/smb restart
```
## 使用注意事项
### 注意环境变量问题
有时我们创建了一个``crontab``，但是这个任务却无法自动执行，而手动执行这个任务却没有问题，这种情况一般是由于在``crontab``文件中没有配置环境变量引起的。

在``crontab``文件中定义多个调度任务时，需要特别注环境变量的设置，因为我们手动执行某个任务时，是在当前``shell``环境下进行的，程序当然能找到环境变量，而系统自动执行任务调度时，是不会加载任何环境变量的，因此，就需要在``crontab``文件中指定任务运行所需的所有环境变量，这样，系统执行任务调度时就没有问题了。

不要假定cron知道所需要的特殊环境，它其实并不知道。所以你要保证在``shell``脚本中提供所有必要的路径和环境变量，除了一些自动设置的全局变量。所以注意如下3点：

1. 脚本中涉及文件路径时写全局路径；
2. 脚本执行要用到``java``或其他环境变量时，通过``source``命令引入环境变量，如:
```
cat start_cbp.sh
!/bin/sh
source /etc/profile
export RUN_CONF=/home/d139/conf/platform/cbp/cbp_jboss.conf
/usr/local/jboss-4.0.5/bin/run.sh -c mev &
```
3. 当手动执行脚本OK，但是``crontab``死活不执行时,很可能是环境变量惹的祸，可尝试在``crontab``中直接引入环境变量解决问题。如:
```
0 * * * * . /etc/profile;/bin/sh /var/www/java/audit_no_count/bin/restart_audit.sh
```

### 注意清理系统用户的邮件日志
每条任务调度执行完毕，系统都会将任务输出信息通过电子邮件的形式发送给当前系统用户，这样日积月累，日志信息会非常大，可能会影响系统的正常运行，因此，将每条任务进行重定向处理非常重要。 例如，可以在``crontab``文件中设置如下形式，忽略日志输出:
```
0 */3 * * * /usr/local/apache2/apachectl restart >/dev/null 2>&1
```
“``/dev/null 2>&1``”表示先将标准输出重定向到``/dev/null``，然后将标准错误重定向到标准输出，由于标准输出已经重定向到了``/dev/null``，因此标准错误也会重定向到``/dev/null``，这样日志输出问题就解决了。

### 系统级任务调度与用户级任务调度
系统级任务调度主要完成系统的一些维护操作，用户级任务调度主要完成用户自定义的一些任务，可以将用户级任务调度放到系统级任务调度来完成（不建议这么做），但是反过来却不行，``root``用户的任务调度操作可以通过”``crontab –uroot –e``”来设置，也可以将调度任务直接写入``/etc/crontab``文件，需要注意的是，如果要定义一个定时重启系统的任务，就必须将任务放到``/etc/crontab``文件，即使在``root``用户下创建一个定时重启系统的任务也是无效的。

### 其他注意事项
新创建的``cron job``，不会马上执行，至少要过2分钟才执行。如果重启cron则马上执行。

当``crontab``失效时，可以尝试``/etc/init.d/crond restart``解决问题。或者查看日志看某个job有没有执行/报错``tail -f /var/log/cron``。

千万别乱运行``crontab -r``。它从``Crontab``目录（``/var/spool/cron``）中删除用户的``Crontab``文件。删除了该用户的所有``crontab``都没了。

在``crontab``中%是有特殊含义的，表示换行的意思。如果要用的话必须进行转义%，如经常用的``date '+%Y%m%d'``在``crontab``里是不会执行的，应该换成``date '+%Y%m%d'``。

更新系统时间时区后需要重启``cron``,在``ubuntu``中服务名为``cron``:
```
$service cron restart
```
``ubuntu``下启动、停止与重启``cron``:
```
$sudo /etc/init.d/cron start
$sudo /etc/init.d/cron stop
$sudo /etc/init.d/cron restart
```