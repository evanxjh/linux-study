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

##### case...esac

##### 函数function功能



#### 循环

------

##### 不定循环 while do done

##### 固定循环 for...do...done

