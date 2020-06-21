## 认识与学习bash

**shell**：操作应用程序的接口

#### shell的变量功能

------

##### 1.变量的显示与设置

- **echo**：变量显示

```
[root@xjh]# echo ${PATH}
```

- **unset**：取消变量名称

若在一串命令中，需要通过其他命令提供的信息，可以使用反单引号命令**‘命令’**或者**$(命令)**。

##### 2.环境变量

- **env**：查看环境变量
- **RANDOM**：大多数的distribution都有随机数生成器，为/dev/random。
- **PS1**：提示符设置

##### 3.变量键盘读取、数组、声明

- **read**

  读取来自键盘输入的变量

- **declare/typeset**

  声明变量的类型，默认类型为字符串

- **array**数组类型

##### 4.变量的删除与替换:yum:

​	使用通配符



#### 命令别名与历史命令

------

##### 1.命令别名设置

- **alias**

```
[root@xjh]# alias lm='ls -l | more'    
```

​		将命令`ls -l | more`用别名`lm`来执行

- **unalias**：

  取消别名的设置

##### 2.历史命令

- **history**

  查询曾经执行过的命令



#### Bash Shell的操作环境

------

##### 1.路径与命令查找顺序

​		系统中有不少的**echo**命令，调用的顺序可以查看

```
[root@xjh]# alias echo='echo -n'	//别名的顺序优先级较高，仅次于以相对/绝对路径执行命令
[root@xjh]# type -a echo		//查看echo的执行顺序
```



##### 2.bash的登录与欢迎界面

```
[root@xjh]# cat /etc/issue
```



##### 3.bash的环境配置文件

- 命令别名、自定义变量在注销bash后就会失效，想要保留，需要将这些设置写入配置文件。

- 区分login shell与non-login shell。

- ~/.bash_profile 只有login-file才会读

- 使用**source**读入环境配置文件:yum:

  ```
  [root@xjh]# source 配置文件名
  
  [root@xjh]# source ~/.bashrc		//source和.是一样的
  [root@xjh]# . ~/.bashrc		
  ```

- ~/.bashrc 只有 non-login shell才会读



##### 4.终端机的环境设置：stty, set

​		可以修改按键，适应用户的使用习惯

- 查看目前的按键内容

```
[root@xjh]# stty [-a]
```

- 修改按键

```
[root@xjh]# stty erase ^h	//将删除字符按键修改为Ctrl+h
```



##### 5.通配符与特殊符号:yum:

| 符号 | 意义                                           |
| ---- | ---------------------------------------------- |
| *    | 代表0个到无穷个任意字符                        |
| ?    | 代表一定有一个任意字符                         |
| []   | 代表一定有一个[]内的字符                       |
| [-]  | 代表在编码顺序内的所有字符                     |
| [^]  | 反向选择，\[^abc]代表一定有一个非a，b，c的字符 |



#### 数据流重定向

------

- `<` 与 `>`可以重定向数据流
  - 1>:以**覆盖**方式将**正确**的数据输出到指定文件；
  - 1>>:以**累加**方式将**正确**的数据输出到指定文件；
  - 2>:以**覆盖**方式将**错误**的数据输出到指定文件；		/dev/null垃圾黑洞
  - 2>>:以**累加**方式将**错误**的数据输出到指定文件。



#### 命令执行的判断依据

------

​		一次性输入多个执行命令

- cmd；cmd不考虑命令相关性的连续执行命令

- `$?`命令回传码，正确执行则会返回`$?=0`的值

- &&与||

  | 命令执行内容   | 说明                                                         |
  | -------------- | ------------------------------------------------------------ |
  | cmd1 && cmd2   | 若cmd1执行完毕且正确，则开始执行cmd2；<br />若cmd1执行完毕且错误，则不执行cmd2。 |
  | cmd1 \|\| cmd2 | 若cmd1执行完毕且正确，则cmd2不执行；<br />若cmd1执行完毕且错误，则开始执行cmd2 |



#### 管道命令:yum:

------

​		管道命令仅能处理**前面一个命令**传来的正确信息。用`|`来连接

##### 1.选取命令：cut和grep

- cut，取出想要的信息

```
[root@xjh]# cut -d'分隔符' -f fields
[root@xjh]# echo $PATH | cut -d ':' -f 5	//将PATH变量取出，找出第五个路径
```

- grep，先分析，若有需要的信息，则取出

```
[root@xjh]# grep [-acinv] [--color=auto] '查找字符串' filename

[root@xjh]# last | grep 'root' 	//将last中有出现root的那一行取出
```



##### 2.排序命令：sort，wc，uniq

- sort 依据不同的数据类型进行排序

```
[root@xjh]# sort [-fbMnrtuk] [file or stdin]
```

- wc 

```
[root@xjh]# wc [-lwm]
[root@xjh]# cat /etc/man.config | wc
查询man.config中有多少相关字、行、字符数
```

- uniq 重复的数据中仅列出一个显示

```
[root@xjh]# last | cut -d ' ' -f1 | sort | uniq -c
使用last将账号列出，仅取出账号列，进行排序后仅取出一位，并统计重复的次数
```



##### 3.双向重定向：tee

```
[root@xjh]# tee [-a] file
```



##### 4.字符转换命令：tr，col，join，paste，expand

- tr 删除一段信息中的文字，或进行文字信息的替换；
- col 转换tab键和处理`/`键；
- join 将两个文件中有相同数据的那一行加在一起；
- paste 将两行贴在一起，中间以`tab`键隔开；
- expand 将`tab`按键转成空格键。



##### 5.切割命令：split

​		将文件依据大小或行数来切割成小文件

```
[root@xjh]# split [-bl] file PREFIX			//-b 大小  -l 行数
```



##### 6.参数代换：xargs

​	产生某个命令的参数

```
[root@xjh]# cut -d':' -f1 /etc/passwd |head -n 3| xarge -p finger
	 -p 为每次执行finger时，都要询问用户
finger root bin daemon? ...y
```

