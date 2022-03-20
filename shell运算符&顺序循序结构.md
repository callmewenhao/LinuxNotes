## 运算符

**基本语法**

`"$((运算式))"`或`$[运算式]`或者 `expr m + n`  // expression表达式

注意 expr 运算符间要有空格，如果希望将expr的结果赋给某个变量，使用""

expr m-n

expr \\*, /, %  // 乘，除，取余

```shell
#!/bin/bash
RES1=$(((2+3)*4))
echo $RES1

RES2=$[2+3*4]
echo $RES2

TEMP=`expr 2 + 3`
RES3=`expr $TEMP \* 4`
echo $TEMP
echo $RES3

SUM=$[$1+$2]
echo sum=$SUM

# 输出，好像无法识别[]
callmewenhao@ubuntu:~$ sh hello.sh 100 200
20
$[2+3*4]
5
20
sum=$[100+200]
```

## if语句

**常用判断条件**

`=` **字符串比较**

**两个整数的比较**

`-lt` 小于

`-le`小于等于

`-eq`等于

`-gt`大于

`-ge`大于等于

`-ne`不等于

```shell
#!/bin/bash
# 单分支
if [ "ok" = "ok" ]
then
        echo "equal!"
fi
# 多分支
if [ $1 -ge 60 ]
then
        echo "great or equal than 60!"
elif [ $1 -lt 60 ]
then
        echo "lower than 60!"
fi
~

callmewenhao@ubuntu:~$ sh hello.sh 60
equal!
great or equal than 60!

```

## case语句

```shell
#!/bin/bash
case $1 in
"1")
echo "Monday!"
;;
"2")
echo "Tuseday!"
;;
*)
echo "other......"
;;
esac

# 运行
callmewenhao@ubuntu:~$ sh hello.sh 1
Monday!
callmewenhao@ubuntu:~$ sh hello.sh 2
Tuseday!
callmewenhao@ubuntu:~$ sh hello.sh 23
other......
```

## for 循环

```shell
#!/bin/bash
for i in "$*"
do
        echo num is $i
done
for i in "$@"
do
        echo num is $i
done
SUM=0
for((i=1; i<=10; i++))
do
        SUM=$[$SUM+$i]
done
echo sum=$SUM

# 运行
callmewenhao@ubuntu:~$ sh hello.sh 1 2 3
num is 1 2 3
num is 1
num is 2
num is 3
hello.sh: 14: Syntax error: Bad for loop variable
callmewenhao@ubuntu:~$ bash hello.sh 1 2 3  # 这里要使用bash
num is 1 2 3
num is 1
num is 2
num is 3
sum=55
```

## while循环

```shell
#!/bin/bash
SUM=0
i=0
while [ $i -le $1 ]
do
        SUM=$[$SUM+$i]
        i=$[$i+1]
done
echo result=$SUM

# 运行
callmewenhao@ubuntu:~$ bash hello.sh 10
result=55
```

## read 读取控制台输入

read(选项)(参数)

选项：

`-p`：指定读取值时的提示符
`-t`：指定读取值时等待的时间（秒），如果没有在指定的时间内输入，就不再等待了。

```shell
#!/bin/bash
read -p "input a number=" NUM1
echo "inputed the number is "$NUM1

callmewenhao@ubuntu:~$ sh hello.sh
input a number=10
inputed the number is 10
```

## 函数

### 系统函数

`basename`基本语法

功能：返回完整路径最后/的部分，常用于获取文件名

`basename [pathname] [suffix]`

功能描述：basename命令会删掉所有的前缀包括最后一个(/)字符，然后将字符串显示出来。

选项:

suffix为后缀，如果suffix被指定了，basename 会将 pathname 或 string 中的 suffix 去掉。

```shell
callmewenhao@ubuntu:~$ basename yolo/a.cpp .cpp
a
```

`dirname`基本语法

功能：返回完整路径最后/的前面的部分，常用于返回路径部分

dirname 文件绝对路径

功能描述：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径（目录的部分）

```shell
callmewenhao@ubuntu:~$ dirname /home/callmewenhao/yolo/a.cpp
/home/callmewenhao/yolo
```

## 自定义函数

```shell
#!/bin/bash
function getSum() {

        SUM=$[$n1+$n2]
        echo sum is $SUM
}
read -p "input a num a1:" n1
read -p "input a num a2:" n2
getSum $n1 $n2


callmewenhao@ubuntu:~$ bash hello.sh
input a num a1:1
input a num a2:2
sum is 3
```

