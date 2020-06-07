## Linux文件与目录管理

#### 目录与路径

------

##### 1.目录相关操作

- **cd**：切换目录
  - cd ~：回到个人的主文件夹内，与仅输入cd效果相同
  - cd -：回到刚才的目录
- **pwd**：显示当前目录
  - `pwd [-p]`加上-p后显示完整路径，不会以连接文件形式显示
- **mkdir**：新建一个新目录
  - `mkdir -m 711 test2`为创建的目录设置权限
  - `mkdir -p test1/test2/test3`递归创建目录
- **rmdir**：删除一个**空**目录
  - `mkdir -p test1/test2/test3`递归删除目录

##### 2.执行文件路径的变量：$PATH

​		`echo $PATH`：显示环境变量



#### 文件与目录管理

------

**ls**：查看文件与目录

```
[root@xjh]# ls [-aAdfFhilnrRSt] 目录名称 
```

- `-a`：全部的文件，连同隐藏文件；
- `-d`：仅列出目录本身；
- `-l`：列出长数据串，包含文件的属性与权限等数据。:yum:

**cp**：复制

```
[root@xjh]# cp [-adfilprsu] source destination 
```

- `-a`:相当于`-pdr`；
- `-i`：若destination已经存在，覆盖时会先询问；
- `-r`：递归地复制，对于目录常用。

**rm**：移除

```
[root@xjh]# rm [-fir] 文件或目录
```

- `-f`：force，强制移除；
- `-i`：移除时进行询问；
- `-r`：递归地移除，**危险操作**。

**mv**：移动

```
[root@xjh]# mv [-fiu] source destination 
```

- `-f`：force，直接覆盖；
- `-i`：移动时进行询问；
- `-u`：update，若source比较新，才会更新。



#### 文件内容查阅

------

##### 1.直接查看内容:yum:

**cat**：由第一行开始显示文件内容

```
[root@xjh]# cat [-AbEnTv] 
```

- `-n`：打印出行号，空白行也有行号

**tac**：最后一行开始显示，与`cat`对应

**nl**：添加行号打印

##### 2.数据选取

**head**：取出前几行

```
[root@xjh]# head [-n number] name 
```

**tail**：取出后面几行

##### 3.非纯文本文件

**od**：读取

```
[root@xjh]# od [-t TYPE] name
```

#####  4.修改文件时间或创建新文件:yum:

- modification time：mtime，文件的“内容”更改时，才会更新这个时间。（**ls的默认时间**）
- status time：ctime，文件的“状态”更改时，才会更新这个时间。
- access time：atime，文件的内容被“取用”时，才会更行这个时间。 

**touch**

```
[root@xjh]# touch [-acdmt] name 
```

- `-a`：仅修改访问时间；
- `-c`：仅修改文件的时间，不存在则不创建新文件；



#### 文件与目录的默认权限与隐藏权限

------

##### 1.默认权限：umast

```
[root@xjh]# umast -S			//0022，是需要减掉的权限
u=rwx,g=rx,o=rx
```

##### 2.文件隐藏属性

**chattr**：设置文件的隐藏属性

```
[root@xjh]# chattr [+-=] [ASacdistu] 文件或目录名称
```

- `-a`：设置a之后，这个文件只能增加数据，不能删除和修改数据，**只有root能设置这个属性**；
- `-i`：让文件不能被删除、改名，设置连接、写入或添加数据，**只有root能设置这个属性**。

**lsattr**：显示文件的隐藏属性

```
[root@xjh]# lsattr [-adR] 文件或目录名称
```

##### 3.特殊权限

**SUID**：出现在文件所有者的x权限上

- 仅对二进制程序有效；
- 执行者对于该程序需要由X的可执行权限；
- 本权限仅在该程序的过程中有效；
- 执行者将具有该程序所有者的权限。

**SGID**：出现在用户组的X权限上，类似于SUID。

**SBIT**：Sticky Bit，仅针对于目录。

- 用户对此目录由w，x权限时，该用户在该目录下创建文件或目录时，仅有自己与root才有权力删除该文件。

##### 4.查看文件类型

```
[root@xjh]# file name
```



#### 命令与文件的查询

##### 1.脚本文件名查询

**which**（寻找“执行文件”）

```
[root@xjh]# which [-a] commond
```

- `-a`：将所有PATH目录中可找到的所有命令均列出

##### 2.文件名的查找

**whereis**（寻找特定文件）

```
[root@xjh]# whereis [-bmsu] 文件或目录名称
```

**locate**:yum:

```
[root@xjh]# locate [-ir] keyword
```

- `-i`：忽略大小写
- `-r`：可以用正则表达式

**find**（参数比较多）

```
[root@xjh]# find [PATH] [Option] [action]
[root@xjh]# find / -mtime 0		//列出过去系统24小时内有改动的文件
[root@xjh]# find /etc -newer /etc/passwd	//列出文件日期比passwd新的文件
```

