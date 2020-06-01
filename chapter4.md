## Centos7.0使用

[centos7.0下载地址](https://www.centos.org/download/)

windows下vmware安装centos7.0：[教程](https://edu.aliyun.com/lesson_1725_13992?spm=5176.8764728.0.0.72c41860Ir1Lht#_13992)

#### :zap:文件系统类型

- ext2/ext3：Linux使用的文件系统类型。
- physical volume(LVM)：弹性调整文件系统大小的一种机制。
- software RAID：软件仿真出磁盘阵列功能。
- swap：内存交换空间：不常被CPU取用的数据会被丢入swap，释放物理内存空间给其他程序。
- vfat：同时被Linux和Windows支持的类型。

------

#### :zap:Window与Terminal切换

tty1~tty6共有6个Terminal让用户登录

切换：**Ctrl+Alt+Fn(n为1-6)**，或者使用**chvt n**

进入图形界面：**Ctrl+Alt+F7**，**startx**

------

#### :zap:命令行模式

`[xjh@www]$ command [-options] parameter1 parameter2 ...`
						 命令 			选项                参数1             参数2

------

#### :zap:常用命令

date：显示日期与时间，**date +%Y/%M/%d**

cal：显示日历， **cal 2020**

bc：计算器，**bc**

sync：数据同步写入磁盘

shutdown：关机命令

reboot：重启

:star: init：切换执行等级，run level：0~7

​			0：关机；1：；2：；3：纯命令行模式；4：；5：含有图形界面模式；6：重启；7：；



------

#### :zap:重要热键

**[Tab]**：命令补全，文件补齐

**[Ctrl]-c**：中断目前程序

**[Ctrl]-d**：代表键盘输入结束，EOF



