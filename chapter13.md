## Shell Script

Shell Script是程序化脚本，用shell的语法来编写脚本，达到想要处理目的。

#### Shell Script编写基础

##### 1.注意事项

- 命令执行从上至下，从左至右；
- 命令、参数间的空白将被忽略；
- 空白行将被忽略；
- 读取到一个`Enter`符号(CR)，尝试开始执行该行（或该串）命令；
- 一行内容太多，可以用`\[Enter]`来扩展到下一行；



##### 2.直接命令执行

​	shell.sh文件必须要具备**rx**权限

​	可用**绝对路径**和**相对路径**来执行，或利用**”PATH“**功能，将shell.sh放入PATH指定的目录内



##### 3.以bash进程来执行

​	 通过”bash shell.sh“ 或”sh shell.sh“来执行。



#### 第一个Shell Script程序

------

```shell
#!/bin/bash							
#Program:							
#		"Hello world!" is the first program.
# 2020/06/22
PATH=/bin:/sbin:/user/bin:/usr/local/bin:/user/local/sbin:~/bin
export PATH
echo -e "Hello World! \a \n"
exit 0
```

- #!/bin/bash声明了使用的shell的名称
- #开始为批注，除了第一行以外。
- 主要环境变量声明，可以在程序中直接执行一些外部命令，而不需要写绝对路径。



##### script执行方式的区别

- 直接执行的方式，`sh script`或 `./script`，其实是在一个新的bash环境（子进程‘）来执行
- 利用`source`来执行，会在原本的bash内生效，因此写入`~/.bashrc`的设置要生效，应使用`source ~/.bashrc`



##### 利用判断符号[]

```
[root@xjh]# [ -z "$HOME" ] ; echo $?	//判断$HOME是否为空
```

- 在中括号内的每个组件都要用空格分隔；
- 中括号内的变量，用双引号括起来；
- 中括号内的常量，用单或双引号括起来。



##### 默认变量$0,$1

- **$#**：代表后接的参数个数；
- **$@**：代表"$1","$2","$3"等，每个变量是独立的；
- **$***：代表”$1c$2c$3c$4“，其中c为分隔符，c默认为空格。



#### 条件判断式

------

##### if...then

```shell
if [ 条件判断式 ]; then
	...				#if中的内容
fi					#用fi来表示结束if
```

​    **多重判断**

```shell
if [ 条件判断式1 ]; then
	...
elif [ 条件判断式2 ]; then
	...
else
	...
fi
```



##### case...esac

```shell
case $变量名称 in
	"第一个变量内容")	   #每个变量用双引号括起来，)为关键字
	;;				    #每个类型结尾用两个连续分号处理
	"第二个变量内容")
	;;
	*)					#用*代笔default
	exit 1
	;;
esac					#用esac代表case的结束
	
```



##### 函数function功能

```shell
function fname() {
	#程序段
}
```

- function也是拥有内置变量的。函数名称代表$0，后续变量为$1,$2...。


#### 循环

------

##### 不定循环 while do done

```shell
while [ condition ] 
do
	...
done
```

##### 不定循环 until do done

```shell
until [ condition ]
do
	...
done
```

- 两者的区别在于，while先判断后执行，until先执行后判断。

##### 固定循环 for...do...done

```shell
for var in con1 con2 con3 ...		#第一次$var为con1，第二次为con2，以此类推
do
	...
done
```

```shell
for (( i=1; i<=$num; i=i+1))
do
	...
done
```

