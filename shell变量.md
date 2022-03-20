## Shell的变量

**Shell 变量介绍**

Linux Shell中的变量分为：系统变量和用户自定义变量。

### 系统变量

`$HOME $PWD $SHELL $USER`等等，比如：`echo $HOME`

显示当前shell中所有变量：`set`

### 用户自定义变量

语法：`变量名=值`，之间无空格

撤销变量：`unset 变量`
声明静态变量：`readonly 变量`，注意：不能 unset

```shell
#!/bin/bash
# 案例1:定义变量A
A=100
# 输出变量需要加上$
echo A=$A
echo "A=$A"
# 案例2:撤销变量Aunset A
echo "A=$A"
# 案例3:声明静态的变量B=2，不能unset
readonly B=2
echo "B=$B"
unset B  # 错误！
```

将命令的返回值赋给变量

A=\`date\`反引号，运行里面的命令，并把结果返回给变量A

A=$(date) 等价于反引号

```shell
#将指令返回的结果赋给变量
c=`date`
D=$(date)
echo "C=$C"
echo "D=$D"
```

### 设置环境变量

**基本语法**

`export 变量名=变量值`（功能描述：将shell变量输出为环境变量/全局变量）

`source 配置文件`（功能描述：让修改后的配置信息立即生效）

`echo $变量名`（功能描述：查询环境变量的值）

快速入门

在/etc/profile文件中定义TOMCAT_HOME环境变量

查看环境变量TOMCAT_HOME的值

在另外一个shell程序中使用TOMCAT_HOME

```shell
# hello.sh:
#!/bin/bash
export CARLA_ROOT=carla
export CARLA_SERVER=${CARLA_ROOT}/CarlaUE4.sh

# 下面向python的搜索路径中添加了两个路径，其中$PYTHONPATH是python的搜索路径，:应该是添加
export PYTHONPATH=$PYTHONPATH:${CARLA_ROOT}/PythonAPI
export PYTHONPATH=$PYTHONPATH:${CARLA_ROOT}/PythonAPI/carla
# 打印路径
echo $CARLA_ROOT
echo $CARLA_SERVER
echo $PYTHONPATH

# 输出
callmewenhao@ubuntu:~$ sh hello.sh
carla
carla/CarlaUE4.sh
:carla/PythonAPI:carla/PythonAPI/carla
```

### 位置参数变量

当我们执行一个shell脚本时，如果希望获取到命令行的参数信息，就可以使用到位置参数变量

比如：./myshell.sh 100 200，这个就是一个执行shell的命令行，可以在myshell脚本中获取到参数信息

**基本语法**

`$n`（功能描述：n为数字，`$0`代表命令本身，`$1-$9`代表第一到第九个参数，十以上的参数需要用大括号包含，如`${10}`）

`$*`（功能描述：这个变量代表命令行中所有的参数，`$*`把所有的参数看成一个整体）

`$@`（功能描述：这个变量也代表命令行中所有的参数，不过`$@`把每个参数区分对待）

`$#`（功能描述：这个变量代表命令行中所有参数的个数）

```shell
# hello.sh:
#!/bin/bash
echo "0=$0, 1=$1, 2=$2"
echo "all paras=$*"
echo "$@"
echo "para nums:$#"

callmewenhao@ubuntu:~$ sh hello.sh 100 200
0=hello.sh, 1=100, 2=200
all paras=100 200
100 200
para nums:2
```

### 预定义变量（略）

