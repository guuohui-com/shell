#Shell脚本

## 1.shell概述

shell 是一种脚本语言

- 脚本：本质是一个文件，文件里面存放的是 特定格式的指令，系统可以使用脚本解析器 翻译或解析 指令 并执行（它不需要编译）
shell 既是应用程序 又是一种脚本语言（应用程序 解析 脚本语言）

- shell命令解析器：
系统提供 shell命令解析器： sh ash bash
查看自己linux系统的默认解析：echo $SHELL

## 2.shell脚本的调用形式
**打开终端时系统自动调用：/etc/profile 或 ~/.bashrc**

/etc/profile
此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行，系统的公共环境变量在这里设置
开始自启动的程序，一般也在这里设置
~/.bashrc
用户自己的家目录中的.bashrc
登录时会自动调用，打开任意终端时也会自动调用
这个文件一般设置与个人用户有关的环境变量，如交叉编译器的路径等等
用户手动调用：用户实现的脚本

## 3.shell语法初识
### 3.1、定义以开头：#!/bin/bash
用来声明脚本由什么shell解释，否则使用默认shell
```shell script
#!/bin/bash
```
### 3.2、单个"#"号代表注释当前行
1.第一步：编写脚本文件
```shell script
#!/bin/bash

#注释
```
2.第二步：加上可执行权限
chmod +x xxxx.sh
```shell script
#!/bin/bash

#注释

chmod +x myshell.sh
echo "test.sh"
```
3.第三步：运行

运行的三种方式：

3.2.1 ./myshell.sh
:先按照 文件中#!指定的解析器解析
如果#！指定指定的解析器不存在 才会使用系统默认的解析器

3.2.2 .myshell.sh
直接使用默认解析器解析（不会执行第一行的#！指定的解析器）但是第一行还是要写的

3.2.3 bash myshell.sh
bash xxx.sh:指明先用bash解析器解析
如果bash不存在 才会使用默认解析器

##4 变量
###4.1 定义变量
定义变量
变量名=变量值
如：num=10

引用变量
$变量名

unset ：清除变量值

示例
```shell script
#!/bin/bash
#注释
chmod +x myshell.sh

num = 10 
echo $num
unset num
echo num
```
###从键盘读取变量 read
1. 示例：
```shell script
#!/bin/bash
#注释
chmod +x myshell.sh
num = 10
echo $num
read num
echo $num
```
2.注意：在一行上显示和添加提示 需要加上-p
示例：
```shell script
#!/bin/bash
#注释
chmod +x myshell.sh
num = 10
echo $num
read -p "请输入变量num" num
echo $num
```
3.一次读取多个值
示例：
```shell script
#!/bin/base
#注释
chmod +x myshell.sh

read data1 data2
echo "data1 = $data1"
echo "data2 = $data2"

```
4.只读变量 readonly

```shell script
#!/bin/base
#只读变量
readonly num = 100
echo "num = $num"
num = 200
echo "num = $num"
```

###5.查看环境变量 env
(1).示例: 
```shell script
#!/bin/base
#只读变量
env
```
(2).导出环境变量
作用：（让其他shell脚本识别该变量，设为全局变量）

(3).source脚本
- source 命令用法： source FileName
- 作用:在当前bash环境下读取并执行FileName中的命令。
- 注:该命令通常用命令“.”来替代。
如:source .bash_rc 与 . .bash_rc 是等效的。
- 注意:source命令与shell scripts的区别是，
source在当前bash环境下执行命令，而scripts是启动一个子shell来执行命令。这样如果把设置环境变量(或alias等等)的命令写进scripts中，就只会影响子shell,无法改变当前的BASH,所以通过文件(命令列)设置环境变量时，要用source 命令。

例：myshell.sh
```shell script
#!/bin/base
#只读变量
export DATA = 250
```
执行文件
```shell script
source myshell.sh
echo $DATA 
```
###6.命名注意事项
- 1、变量名不能以数字开头

1_num=10 错误

num_1=20 正确
- 2、等号两边不能直接接空格符，若变量中本身就包含了空格，则整个字符串都要用双引号、或单引号括起来
- 3、双引号 单引号的区别

双引号：可以解析变量的值

单引号：不能解析变量的值

例：
```shell script
#!/bin/base
num=200
echo "num = $num"
echo 'num = $num'
```

执行结果
```shell script
num = 200
num = $num
```













