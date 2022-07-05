# Linux

## Linux介绍

linux是一个开源、免费的操作系统

## 网络连接的三种模式
1. 桥接模式，虚拟系统可以和外部系统通讯，但是容易造成IP冲突
2. NAT模式，网络地址转换模式，虚拟系统可以和外部系统通讯，不造成IP冲突
3. 主机模式：独立的系统

## 虚拟机克隆（用于集群）
* 方式1，直接拷贝一份安装好的虚拟机文件
* 方式2，使用vmware的克隆操作，注意，克隆时，需要先关闭linux系统

## 虚拟机快照
在使用虚拟机系统的时候，想回到原先的某个状态，也就是说担心可能有些误操作造成系统异常，需要回到原先某个正常运行的状态，就用快照管理。
<img src="images/2022-05-23-23-15-59.png" style="zoom:67%;">
<img src="images/2022-05-23-23-19-04.png" style="zoom:67%;">
<img src="images/2022-05-23-23-20-45.png" style="zoom:67%;">
要想恢复：
<img src="images/2022-05-23-23-22-10.png" style="zoom:67%;">

## 虚拟机的迁移和删除
直接拷贝或剪切虚拟系统的文件夹，删除就直接删除那个文件夹

## 安装vmtools
可以设置windows和centos的共享文件夹
<img src="images/2022-05-24-01-02-09.png" style="zoom:67%;">
注意：
1. 如果虚拟机->重新安装vmtools变灰，则关机，在开机之后开机完成之前就会变黑
2. 第八点，除了一个不用默认设置，输入no
<img src="images/2022-05-24-01-08-47.png" style="zoom:67%;">
### 设置共享文件夹
<img src="images/2022-05-24-01-11-09.png" style="zoom:67%;">

## Linux目录结构
采用层级式的树状目录结构，最上层是根目录“/”，然后在此目录下的其他目录是固定的
在Linux世界，一切皆文件（连硬件也映射成文件）
### 具体的目录结构
<img src="images/2022-05-24-01-43-55.png" style="zoom:67%;">
<img src="images/2022-05-24-01-45-53.png" style="zoom:67%;">
<img src="images/2022-05-24-01-48-00.png" style="zoom:67%;">
<img src="images/2022-05-24-01-49-24.png" style="zoom:67%;">

## 远程登录Xshell
下载后文件->新建
主机输入Linux的ip地址（可以用ifconfig获得）
<img src="images/2022-05-24-02-13-42.png" style="zoom:67%;">
<img src="images/2022-05-24-02-14-39.png" style="zoom:67%;">
主机一定要是Linux的ip地址，名称可以随便写，之后点击确定就行。
双击新建的会话即可完成连接

## 远程文件传输Xftp
跟上述类似
<img src="images/2022-05-24-02-30-23.png" style="zoom:67%;">

## vim
### 常用的三种模式
<img src="images/2022-05-25-00-22-40.png" style="zoom:67%;">
<img src="images/2022-05-25-00-23-59.png" style="zoom:67%;">
### 快捷键
<img src="images/2022-05-25-00-25-08.png" style="zoom:67%;">
<img src="images/2022-05-25-00-26-02.png" style="zoom:67%;">

## 关机重启命令
<img src="images/2022-05-28-13-56-19.png" style="zoom:67%;">

## 用户登录和注销
登录时尽量少用root登录，可以用普通用户登录，再用“su - 用户名”切换到root
输入logout即可注销用户
<img src="images/2022-05-28-14-11-29.png" style="zoom:67%;">

## 用户管理
### 添加用户
useradd 用户名：当创建用户成功后，会自动创建和用户同名的家目录
<img src="images/2022-05-28-17-41-42.png" style="zoom:67%;">
useradd -d 指定目录 新的用户名：给新创建的用户指定家目录
<img src="images/2022-05-28-17-44-01.png" style="zoom:67%;">

### 指定/修改密码
passwd 用户名
<img src="images/2022-05-28-17-47-30.png" style="zoom:67%;">
显示当前用户所在的目录：pwd
<img src="images/2022-05-28-17-55-05.png" style="zoom:67%;">

### 删除用户
userdel 用户名：删除用户，但保留家目录
<img src="images/2022-05-28-18-04-12.png" style="zoom:67%;">
userdel -r 用户名：删除用户和家目录
<img src="images/2022-05-28-18-06-33.png" style="zoom:67%;">
一般情况下，建议保留家目录

### 查询用户信息
id 用户名
当用户不存在时，返回无此用户
<img src="images/2022-05-30-13-56-28.png" style="zoom:67%;">

### 切换用户
su - 切换用户名
权限高切换到权限低不需要输密码，反之需要
当需要返回到原来用户时，输入exit/logout
<img src="images/2022-05-30-14-23-34.png" style="zoom:67%;">

### 查看当前用户/登录用户
who am i
<img src="images/2022-05-30-14-30-39.png" style="zoom:67%;">

### 用户组
类似于角色，对有共性/权限的多个用户进行统一管理

### 新增组
groupadd 组名
<img src="images/2022-05-30-16-39-30.png" style="zoom:67%;">

### 删除组
groupdel 组名
<img src="images/2022-05-30-16-40-52.png" style="zoom:67%;">

### 增加用户时直接加上组
useradd -g 组名 用户名
<img src="images/2022-05-30-16-48-47.png" style="zoom:67%;">

### 修改用户的组
usermod -g 组名 用户名
<img src="images/2022-05-30-17-01-44.png" style="zoom:67%;">

### 用户和组相关文件
<img src="images/2022-05-30-20-12-40.png" style="zoom:67%;">
<img src="images/2022-05-30-20-15-48.png" style="zoom:67%;">
<img src="images/2022-05-30-20-16-51.png" style="zoom:67%;">
zwj没有设置密码，设置密码后：
<img src="images/2022-05-30-20-18-31.png" style="zoom:67%;">
<img src="images/2022-05-30-20-19-55.png" style="zoom:67%;">

## 指定运行级别
<img src="images/2022-05-31-02-43-30.png" style="zoom:67%;">

init [0123456]
<img src="images/2022-05-31-02-45-35.png" style="zoom:67%;">
<img src="images/2022-05-31-02-47-04.png" style="zoom:67%;">
<img src="images/2022-05-31-02-47-43.png" style="zoom:67%;">

<img src="images/2022-05-31-02-53-05.png" style="zoom:67%;">
<img src="images/2022-05-31-02-56-21.png" style="zoom:67%;">

## 找回root密码
<img src="images/2022-05-31-03-04-08.png" style="zoom:67%;">
<img src="images/2022-05-31-03-04-51.png" style="zoom:67%;">
<img src="images/2022-05-31-03-05-35.png" style="zoom:67%;">
<img src="images/2022-05-31-03-06-17.png" style="zoom:67%;">

## 帮助指令
man 获得帮助信息
man [命令或配置文件]（功能描述：获得帮助信息）
<img src="images/2022-05-31-03-18-29.png" style="zoom:67%;">
<img src="images/2022-05-31-03-17-56.png" style="zoom:67%;">

在linux下，隐藏文件以.开头
选项可以组合使用，如：
<img src="images/2022-05-31-03-19-38.png" style="zoom:67%;">

help指令（功能描述：获得shell内置命令的帮助信息）
<img src="images/2022-05-31-03-22-13.png" style="zoom:67%;">

## 文件目录指令
pwd：显示当前工作目录的绝对路径
<img src="images/2022-05-31-03-51-17.png" style="zoom:67%;">

ls [选项] [目录或文件]
<img src="images/2022-05-31-03-53-39.png" style="zoom:67%;">

cd ~ 或 cd ：回到家目录
cd ..：回到上级目录
<img src="images/2022-05-31-04-05-33.png" style="zoom:67%;">
<img src="images/2022-05-31-04-06-13.png" style="zoom:67%;">

mkdir用于创建目录
mkdir [选项] 要创建的目录
<img src="images/2022-05-31-04-14-13.png" style="zoom:67%;">

-p：创建多级目录
<img src="images/2022-05-31-04-16-11.png" style="zoom:67%;">

rmdir [选项] 要删除的空目录：删除空目录
<img src="images/2022-05-31-04-21-51.png" style="zoom:67%;">

rm -rf 要删除的目录：删除非空目录
<img src="images/2022-05-31-04-22-51.png" style="zoom:67%;">

touch 文件名称：创建一个空文件
<img src="images/2022-05-31-04-25-37.png" style="zoom:67%;">

cp：拷贝文件到指定目录
cp [选项] source dest
<img src="images/2022-05-31-16-45-42.png" style="zoom:67%;">

-r：递归复制整个文件夹
<img src="images/2022-05-31-16-48-31.png" style="zoom:67%;">

强制覆盖不提示：\cp
<img src="images/2022-05-31-16-51-02.png" style="zoom:67%;">

rm：移除文件或目录
rm [选项] 要删除的文件或目录
<img src="images/2022-05-31-17-02-09.png" style="zoom:67%;">
-r：递归删除整个文件夹
-f：强制删除不提示
<img src="images/2022-05-31-17-04-53.png" style="zoom:67%;">

mv：移动文件与目录或重命名
mv oldNameFile newNameFile（重命名）
<img src="images/2022-06-01-05-37-41.png" style="zoom:67%;">

mv /temp/movefile /targetFolder（移动文件）
<img src="images/2022-06-01-05-41-06.png" style="zoom:67%;">

移动整个目录
<img src="images/2022-06-01-05-44-02.png" style="zoom:67%;">

可以移动目录或文件的同时重命名

cat：查看文件内容，不能修改
cat [选项] 要查看的文件
-n：显示行号
<img src="images/2022-06-01-05-52-20.png" style="zoom:67%;">

为了浏览方便，会带上管道命令 | more
<img src="images/2022-06-01-05-54-40.png" style="zoom:67%;">

more 要查看的文件
<img src="images/2022-06-01-05-58-14.png" style="zoom:67%;">
<img src="images/2022-06-01-05-59-46.png" style="zoom:67%;">

less 要查看的文件
<img src="images/2022-06-01-06-04-21.png" style="zoom:67%;">
<img src="images/2022-06-01-06-06-42.png" style="zoom:67%;">

echo输出内容到控制台
echo [选项] 输出内容
<img src="images/2022-06-01-06-11-11.png" style="zoom:67%;">

head用于显示文件的开头部分，默认显示前十行
head 文件（显示前十行）
<img src="images/2022-06-01-06-16-36.png" style="zoom:67%;">

head -n 5 文件（显示前5行，5可以是任意行数）
<img src="images/2022-06-01-06-20-05.png" style="zoom:67%;">

tail用于显示文件的尾部，默认显示后十行
tail 文件（显示后10行）
<img src="images/2022-06-01-06-28-00.png" style="zoom:67%;">

tail -n 5 文件（显示后5行，5可以是任意行数）
<img src="images/2022-06-01-06-29-14.png" style="zoom:67%;">

tail -f 文件（实时追踪该文档的所有更新）
<img src="images/2022-06-01-06-36-43.png" style="zoom:67%;">
<img src="images/2022-06-01-06-37-18.png" style="zoom:67%;">
退出是Ctrl+C

\>重定向（覆盖）和>>追加
ls -l > 文件 （覆盖写）
<img src="images/2022-06-01-06-51-04.png" style="zoom:67%;">
文件没有会自动创建

ls -al >> 文件 （追加）
<img src="images/2022-06-01-06-53-00.png" style="zoom:67%;">

cat 文件1 > 文件2 （将文件1内容覆盖到文件2）
<img src="images/2022-06-01-06-54-45.png" style="zoom:67%;">

echo "内容" >> 文件 （追加）

ln：软链接也叫符号链接，类似于快捷方式

ln -s [原文件或目录] [软链接名]（给原文件创建一个软链接）
<img src="images/2022-06-01-17-59-04.png" style="zoom:67%;">
<img src="images/2022-06-01-18-01-25.png" style="zoom:67%;">

删除软链接
请注意：命令更改为rm /home/myroot（如果用下面的命令会连指向的目录下的所有文件都被删掉）
<img src="images/2022-06-01-18-04-28.png" style="zoom:67%;">

history：查看已执行过的历史指令
<img src="images/2022-06-01-18-10-16.png" style="zoom:67%;">

history 10：显示最近执行过的10条指令
<img src="images/2022-06-01-18-11-34.png" style="zoom:67%;">

执行编号为138的历史指令
<img src="images/2022-06-01-18-13-23.png" style="zoom:67%;">

date：显示当前日期
<img src="images/2022-06-02-00-24-41.png" style="zoom:67%;">

date +%Y：显示当前年份
<img src="images/2022-06-02-00-29-35.png" style="zoom:67%;">

date +%m：显示当前月份
<img src="images/2022-06-02-00-30-36.png" style="zoom:67%;">

date +%d：显示当前是哪一天
<img src="images/2022-06-02-00-31-32.png" style="zoom:67%;">

显示当前年月日
<img src="images/2022-06-02-03-20-35.png" style="zoom:67%;">

显示当前年月日时分秒
<img src="images/2022-06-02-03-22-24.png" style="zoom:67%;">

date -s 字符串时间：设置系统当前时间
<img src="images/2022-06-02-03-29-51.png" style="zoom:67%;">

cal：显示本月日历
<img src="images/2022-06-02-03-32-58.png" style="zoom:67%;">

cal 2022：显示2022年日历
<img src="images/2022-06-02-03-33-34.png" style="zoom:67%;">

<img src="images/2022-06-02-03-40-59.png" style="zoom:67%;">
<img src="images/2022-06-02-03-43-32.png" style="zoom:67%;">
<img src="images/2022-06-02-03-46-02.png" style="zoom:67%;">
<img src="images/2022-06-02-03-47-46.png" style="zoom:67%;">

ls -lh（h：以人类看得懂的单位显示）
<img src="images/2022-06-02-03-51-54.png" style="zoom:67%;">

locate指令快速定位文件路径，由于建立了自己的数据库，所以查询速度很快
locate 搜索文件
注意：第一次运行前，必须使用updatedb指令创建locate数据库
<img src="images/2022-06-02-04-00-40.png" style="zoom:67%;">

which：可以查看某个指令在哪个目录下
<img src="images/2022-06-02-04-02-49.png" style="zoom:67%;">

grep过滤查找，管道符，"|"，表示将前一个命令的处理结果输出传递给后面的命令处理
grep [选项] 查找内容 源文件
-n：显示匹配行及行号
-i：忽略字母大小写
<img src="images/2022-06-02-04-53-52.png" style="zoom:67%;">
<img src="images/2022-06-02-04-54-45.png" style="zoom:67%;">

gzip 文件：压缩文件，只能将文件压缩为*.gz文件
<img src="images/2022-06-02-05-00-42.png" style="zoom:67%;">

gunzip 文件.gz：解压缩文件
<img src="images/2022-06-02-05-02-05.png" style="zoom:67%;">

zip [选项] XXX.zip 将要压缩的内容（压缩文件和目录）
-r：递归压缩，即压缩目录
<img src="images/2022-06-02-05-13-05.png" style="zoom:67%;">

unzip [选项] XXX.zip（解压缩文件）
-d 目录：指定解压后文件的存放目录
<img src="images/2022-06-02-05-17-55.png" style="zoom:67%;">

tar
<img src="images/2022-06-02-05-27-09.png" style="zoom:67%;">

压缩文件
<img src="images/2022-06-02-05-29-57.png" style="zoom:67%;">
<img src="images/2022-06-02-05-31-22.png" style="zoom:67%;">

解压缩文件
<img src="images/2022-06-02-05-33-21.png" style="zoom:67%;">
解压到指定目录
<img src="images/2022-06-02-05-39-23.png" style="zoom:67%;">

## 组管理和权限管理
在linux中每个用户必须属于一个组，每个文件有所有者、所在组和其他组的概念。
<img src="images/2022-06-03-04-15-02.png" style="zoom:67%;">

### 所有者
一般为文件的创建者
查看文件的所有者
<img src="images/2022-06-03-11-46-58.png" style="zoom:67%;">
前面的那一列为所有者

修改文件所有者
chown 用户名 文件名
<img src="images/2022-06-03-11-50-03.png" style="zoom:67%;">
<img src="images/2022-06-03-11-52-12.png" style="zoom:67%;">

-R：如果是目录，则使其下所有子文件或目录递归生效
<img src="images/2022-06-04-16-16-27.png" style="zoom:67%;">
<img src="images/2022-06-04-16-17-02.png" style="zoom:67%;">
<img src="images/2022-06-04-16-18-55.png" style="zoom:67%;">
<img src="images/2022-06-04-16-19-33.png" style="zoom:67%;">
chown newowner:newgroup 文件/目录（改变所有者和所在组）


### 所在组
查看文件所在组
<img src="images/2022-06-03-12-07-04.png" style="zoom:67%;">
<img src="images/2022-06-03-15-06-38.png" style="zoom:67%;">
后面的一列为所在组

修改文件所在的组
chgrp 组名 文件名
<img src="images/2022-06-03-15-11-55.png" style="zoom:67%;">
<img src="images/2022-06-03-15-12-45.png" style="zoom:67%;">
<img src="images/2022-06-03-15-13-28.png" style="zoom:67%;">

-R：如果是目录，则使其下所有子文件或目录递归生效
<img src="images/2022-06-04-16-27-20.png" style="zoom:67%;">
<img src="images/2022-06-04-16-28-21.png" style="zoom:67%;">
<img src="images/2022-06-04-16-28-50.png" style="zoom:67%;">
<img src="images/2022-06-04-16-29-49.png" style="zoom:67%;">

改变用户所在组
usermod -g 新组名 用户名
<img src="images/2022-06-03-15-31-36.png" style="zoom:67%;">
usermod -d 新目录 用户名：改变用户的家目录。**特别说明**：用户有进入到新目录的权限

### 权限的基本介绍
<img src="images/2022-06-03-18-33-35.png" style="zoom:67%;">

### rwx权限详解
<img src="images/2022-06-03-18-38-03.png" style="zoom:67%;">
<img src="images/2022-06-03-18-47-10.png" style="zoom:67%;">

### 修改权限
chmod：修改文件或目录的权限
u：所有者 g：所在组 o：其他组 a：所有人
chmod u=rwx,g=rx,o=x 文件/目录名
<img src="images/2022-06-04-15-39-01.png" style="zoom:67%;">
<img src="images/2022-06-04-15-41-48.png" style="zoom:67%;">
chmod o+w 文件/目录名
<img src="images/2022-06-04-15-45-14.png" style="zoom:67%;">
chmod a-x 文件/目录名
<img src="images/2022-06-04-15-48-16.png" style="zoom:67%;">

通过数字变更权限
r=4 w=2 x=1 rwx=4+2+1=7
chmod u=rwx,g=rx,o=x 文件/目录名
相当于chmod 751 文件/目录名
<img src="images/2022-06-04-16-04-47.png" style="zoom:67%;">
<img src="images/2022-06-04-16-05-28.png" style="zoom:67%;">
