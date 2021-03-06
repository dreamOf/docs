###  一、Linux是什么？

         Linux读音：英 ['lɪnəks]  美 ['lɪnəks]
    
       Linux是一款操作系统，免费、开源、安全、高效、稳定且处理并发非常强悍。许多的企业级应用都会部署到Linux系统的服务器上。

### 二、Linux与windows的区别

### 三、Linux的学习方向

1. Linux运维工程师
2. Linux嵌入式开发工程师
3. Linux系统中开发程序

### 四、Linux应用领域

   1.桌面

   2.服务器

   3.嵌入式

### 五、学习方法

**第一阶段：**Linux基本命令操作。

         - 文件操作命令（rm mkdir chmod  chown）
         - 编辑工具使用（vi vim）
         - 用户管理

**第二阶段：**Linux的各种配置

- 环境变量配置

- 网络配置

- 服务配置

**第三阶段：**Linux搭建开发环境

**第四阶段：**Linux的shell命令编写，对linux服务器进行维护

**第五阶段：**Linux的安全配置，保障服务的正常运行，能对系统进行调优

**第六阶段：**深入理解Linux系统，熟悉掌握大型网站应用架构组成，并熟悉各个环节的部署和维护

### 六、Linux基础篇

- #### vm和centos的安装

  **第一步**：安装vm。

  **第二步**：安装centos.

- #### 实现共享文件夹

  #### vmware使用vmtool实现复制和粘贴功能，并实现文件夹的共享，由于本人使用的是virtualBox，此处只记录virtualBox的实现过程：

  1）在virtualBox的设备中安装增强设备。注意事项：需要右击cd图标，并弹出。

  2）增加共享文件夹。共享的文件夹是母机的文件夹，比如文件夹的名字为：share。

  3) 在命令行中，输入如下命令：

  ```shell
  mkdir /mnt/myshare
  mount -t vboxsf share  /mnt/myshare
  ```

  *在linux中增加文本信息后，提示文件正忙？

  **Linux的目录结构**

linux采用的是级层式的树状目录结构，此结构中最上层为根目录“/”；所有文件都在根目录下。

主要目录介绍：

- bin目录：是Binary的缩写，存放着经常使用的的命令。

- sbin目录：是super user的缩写。存放系统管理员存放的系统管理工具。

- home目录：存放普通用户的目录。目录以用户名命令。

- root目录：存放的是系统管理员。

- lib目录：系统开机所需要的最基本的动态链接功效库。其作用类似于windows里面的dll文件。几乎所有的文件都要用到这些功效库。

- lost+found目录：当系统非法关机后，该目录下会存放一些文件。一般情况下，该文件为空。

- etc目录：所有系统管理所需要的配置文件和子目录。

- user目录：用户的很多应用程序和文件都放在这个目录下，类似与windows的program file目录。

- boot目录：存放linux启动时的一些核心文件，包括一些连接文件和镜像文件。

- proc目录：这个目录是一个虚拟目录，是系统内存的映射，访问这个目录来获取系统信息。

- svr目录：service的缩写，该目录存放一些服务启动之后需要提取的数据。

- sys目录：这是linux2.6内核的一个很大变化。该目录安装了2.6内核中的新出现的一个文件系统。

- tmp目录：用来存放临时文件。

- dev目录：类似于windows的设备管理器。把所有的 硬件用文件形式存储。

- media目录：linux会自动识别一些设备。比如U盘、光驱等。识别后linux会把设别的设备挂在到这个目录下。

- mnt目录：让用户临时 挂在别的文件系统的，我们可以把外部的存储挂载到这个目录下。

- opt目录：给主机额外安装软件所摆放的目录。如安装ORACLE 数据库可放到该目录下。默认为空。

- user/local目录：这是另外一个给主机额外安装软件所安装的目录。**一般是通过编译源码方式安装的程序**。

- var目录：这个目录存放着不断扩充的东西，习惯将经常被修改的目录放在这个目录下。包括各种日志文件。

- selinux目录：他是一个安全子系统，它能控制程序只能访问特定文件。

  **linux中只有一个根目录。**

  **linux中各个目录的内容是规划好的，不要乱放**

  **linux是通过文件管理设备的，因此linux系统，一切皆文件。**

  **linux各个文件目录下存放什么内容，必须要有一定的认识。**

  **学习后，脑海中有linux的目录印象。**

### 七、Linux实操篇

####   1.远程登录和文件上传下载

  因为linux一般都安装在服务器上，我们需要通过远程工具来操作linux服务器，发送linux命令。

 初使virtualBox的坑：第一次使用virtualBox的时候，网络连接的方式使用的是网络地址连接（NAT），该方式默认母机无法访问虚拟机的网络。安装了xshell远程工具后，怎么也连不上linux系统，整整郁闷了一下午。后来，在不经意间看到了virtualBox的网络连接方式的详解，了解到各个连接方式的区别，终于知道为何连不上了。

| 网络连接方式     | NAT  | 桥接 | internal     | HOST-ONLY |
| ---------------- | ---- | ---- | ------------ | --------- |
| 虚拟机—>主机     | 是   | 是   | 否           | 否        |
| 主机—>虚拟机     | 否   | 是   | 否           | 否        |
| 虚拟机—>其他主机 | 是   | 是   | 否           | 否        |
| 其他主机—>虚拟机 | 否   | 是   | 否           | 否        |
| 虚拟机之间       | 否   | 是   | 同网络下可以 | 是        |

NAT方式下，如果要使主机能访问虚拟机，需要配置端口转发，主机ip为主机（母机）的ip，子系统的ip为虚拟机的ip，子系统的端口为22,填好转发规则后，在xshell里把ip配置成主机的ip，端口号配置成主机的端口号，这样就能转发到虚拟机的网络了。

- xshell5：远程登陆软件，发送发送命令。流畅度高、完美解决了中文乱码。是首选的远程工具。注意:需要开启sshd服务（22端口）。

- xftp5:用于远程文件上传和下载。

#### 2.vi和vim

1)、vi:类似于文本编辑器。

vim：增强版的vi，有自动提示的功能。

 vi和vim常用的三种模式：

- 正常模式

  这是默认模式。该模式下，可以使用上下左右键来移动光标。你可以使用“删除字符”和“删除整行”来处理档案内容，也可以使用“复制、粘贴”处理你的文件数据。

- 插入模式

  按下i、l、o、O、a、A、r、R等，任何一个字母之后才会进入编辑模式，一般按i即可。

- 命令行模式

  该模式中提供相关指令，完成读取、存盘、替换、离开vim、显示行号、等的动作。

2）、vi或者vim模式的相互转换

+ 命令行:vim xxx --->一般/正常模式--->i或a--->一般/编辑模式---esc--->一般/编辑模式-->:或者/-->命令模式-->:qw！
+ 命令模式-->esc-->一般/编辑模式。

3）vi或者vim的快捷键

+ **yy** 拷贝当前行。拷贝当前行向下的5行用：5yy,并粘贴（p）。
+ **dd** 删除当前行。删除当前行向下的5行用：5dd.
+ **/关键字** 回车查找，输入n查找下一个。
+ **:set nu 和 :set nonu** 设置文件的行号和取消文件的行号。
+ **G和gg** 编辑/etc/profile文件到最末行或者首行。 
+ **shift:g** 编辑/etc/profile文件，将光标移动到20行。
+ 更多请参照文档。

#### 3.开机重启和注销

- shutdown

  ```shell
  shutdown -h now                       --立即关机
  shutdown -h 1                         --1分钟后关机
  shutdown -r now                       --立即重启
  ```

- halt

  ```shell
  halt                                  --等价于关机
  ```

- reboot

  ```shell
  reboot                                --重启计算机
  ```

- syn

  ```shell
  syn                                  --把内存数据同步到磁盘
  ```

注意：关机或者重启之前，应该先执行syn命令，把未保存的数据保存到磁盘，防止数据丢失。

- logout

```shell
logout                                    --注销用户
```

注意：logout在图形界面的终端下，是无效的。在运行级别3下有效。

#### 4.用户管理

Linux是一个多用户多任务的操作系统， 任何一个要使用系统资源的用户，都必须向系统管理员申请一个账号，然后这个账号才能进入系统。

linux用户至少需要一个组。

##### 1） 用户

- 添加用户

```shell
useradd [选项] 用户名
useradd -d 目录名 用户名
```

说明：用户创建后，默认创建一个以用户名为名的组，并把该用户放到该组。

           可以通过 useradd -d 指定目录。

- 指定/修改密码

```shell
passwd 用户名
```

- 删除用户

```shell
userdel 用户名
```

- 查询用户

```shell
id 用户名                         --查某一个用户
whoami                           --查当前用户
```

- 切换用户

```
su - 用户名
```

切换用户后，用exit命令退出。

##### 2）用户组

类似于角色，把某一类的用户可以放到同一个组。

- 增加组

```shell
groupadd 组名                          --创建一个组
groupdel 组名                          --删除一个组
```

创建用户时，直接指定组：

```
useradd -g 组名 用户名                 --增加用户时，指定组名
useradd -d 组名 用户名                 --增加用户时，创建组名
```

- 修改组

```shell
usermod -g 组名 用户名
```

##### 3）用户和组的相关文件

- /etc/passwd 文件

  用户的配置文件，记录用户的各种信息；

  每行的含义：用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录shell。

  例：sq_chen:x:1000:1000:sq_chen:/home/sq_chen:/bin/bash

- etc/shadow 文件

  口令/密码的配置文件

  每行的含义：登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志。

  例：sq_chen:$6$nZLMpbTsdxihOAUU$Nk3dNGuQ1PrCQ8H9JQfSXb4vqzkbLLtWVsWbK0Xzau9tXfdHUBY89lx0JesJgS0BO4hAjArteOGdw7EF0R366/:17749:0:99999:7:::

- etc/group 文件

  组的配置文件，记录linux包含的组信息。

  每行含义：组名:口令:组标识号:组内用户列表。

  例：wheel:x:10:sq_chen，组的用户名是看不见的？

#### 5.使用指令

##### 1）指定运行级别

```java
0:关机
1:单用户【找回密码】
2:多用户状态，没有网络服务
3:多用户状态，有网络服务
4:系统未使用保留给用户，暂时未开放
5:图形界面
6:系统重启
```

在/etx/inittab中可以查看运行级别信息.

切换到指定运行级别的指令：

```shell
init 级别
```

**？？？**如何找回丢失的root密码

思路:进入到单用户模式，然后修改密码。因为进入单用户模式，root不需要密码就可以登录。

答：开机，在引导时回车，看到一个界面输入小e，看到一个新的界面高亮到选中第二行（编辑内核），在输入小e,在这行输入1，再输入 回车，再次输入b，进入到单用户模式，使用passwd指令修改root密码。

##### 2）帮助指令

当我们对某个指令不熟悉的时候，我们可以通过帮助指令来熟悉命令。

- man

```shell
man 指令
```

- help

```shell
help 指令
```

##### 3）文件目录类

```shell
pwd      --当前目录的绝对路径

ls       --显示当前目录或者文件
ls -a    --显示当前目录的所有文件
ls -l    --以列表的方式显示信息
ls -al   --显示当前目录的所有文件包含隐藏文件

cd  参数     --切换目录
cd ~         --回到home目录(cd 也能回到home目录)
cd ..        --回到当前目录的上级目录

mkdir [选项] 目录      --创建目录
mkdir -p 目录			--创建多级目录

rmdir [选项] 目录	   --删除目录，不能删除非空目录
rm -rf 目录            --删除非空目录

touch 文件名            --创建空文件
touch 文件名1，文件名2   --创建多个空文件

cp [选项] sorce dest    --拷贝文件，例子：cp aaa.txt /home
cp -r sorce dest        --递归拷贝整个文件夹
\cp -r sorce dest	    --强制覆盖，不会提示

rm [选项] 文件/目录     --删除文件。默认删除空文件或目录
rm -r 文件/目录         --递归删除整个文件夹
rm -f 文件/目录         --强制删除

mv 文件夹/文件 文件夹/文件  --移动文件/重命名，如果后面的目录中不存在就为移动

cat [选项] 文件       --查看文件内容，只能看，不能改
cat -n 文件           --显示文件的行号
cat -n 文件 | more    --分页显示

more 文件  --以全屏的方式，按页显示内容

less 文件 --与more指令相似，分屏查看内容，它并不是一次性打开文件，而是根据需要加载内容，显示大文件具有较高的效率。

>输出重定向和>>追加
ls -l > 文件        --将ls -l命令显示的内容写入文件a.txt中（如果a.txt不存在就创建，否则覆盖写）
ls -al >> 文件      --将ls -al命令显示的内容追加到文件a.txt中
cat 文件1 > 文件2    --将文件1的内容覆盖到文件2
echo "内容" >> 文件

echo [选项] [输出内容]   --输出内容到控制台
echo $PATH     --输出环境变量
echo "hello"   --输出内容hello

head 文件命名     --显示前十行
head -n 5 文件名  --显示前5行

tail 文件      --显示文件的后10行
tail -n 5 文件 --显示文件的后5行
tail -f 文件   --实时追踪该文件的所有更新【用Ctrl+c 退出】

ln -s [原文件或目录] [软链接名]     --软链接，类似于windows的快捷方式
in -s /root linkToRoot            --虽然连接到root目录下了，但是pwd还是当前软链接所在路径
rm -rf linkToRoot                 --删除软链接，用rm linkToRoot会提示错误，因为系统认为下面有文件

history         --查看已经执行过的所有指令，也可以执行历史指令
history 10      --前10个指令
!178            --执行历史编号178的指令


```

more命令下的快捷键

| 操作   | 功能说明                      |
| ------ | ----------------------------- |
| space  | 向下翻一页                    |
| enter  | 向下翻一行                    |
| q      | 立刻离开more,不再显示文件内容 |
| Ctrl+f | 向下滚动一屏                  |
| Ctrl+B | 返回上一屏                    |
| =      | 输出当前行号                  |
| :f     | 输出文件名和当前行号          |

#####  4）日期时间类

```shell
date        --显示当前时间
date "+%Y"  --显示年度
date "+%m"  --显示月
date "+%d"  --显示日
date "+%Y %m %d %H:%M:%S"  --年月日时分秒

date -s 字符串时间  设置日期格式
date -s "2018-01-01 11:25:12"

cal 
```

##### 5）搜索查找类

```shell
find [搜索范围] [选项] 
```

##### 6）压缩和解压缩类

```shell
gzip 文件          --压缩文件为*.gz文件，压缩完文件后，原来的文件会消失
gunzip 文件.gz     --解压缩文件.gz，解压缩后源文件也会消失

zip [选项] 压缩文件 目录/文件  
unzip [选项] 文件.zip 
zip -r mypackage.zip /home  --把home目录下的所有文件压缩到mypackage.zip
unzip -d /opt/tmp mypackage.zip

tar [选项] xxx.tar.gz 打包内容                  --打包指令
tar -zcvf a.tar.gz a.txt b.txt                --把a.txt和b.txt压缩到a.tar.gz
tar -zcvf a.tar.gz /home                      --把home文件夹压缩到a.tar.gz
tar -zxvf a.tar.gz                            --解压a.tar.gz到当前目录
tar -zxvf a.tar.gz -c /opt                    --将a.tar.gz解压到opt文件夹下【指定的目录必须存在】
```

参数详解：

| 简称 | 全称    | 功能描述                                 |
| ---- | ------- | ---------------------------------------- |
| z    | gzip    | 执行或者压缩文件                         |
| c    | create  | 创建新文件                               |
| v    | verbose | 详细列出处理的文件                       |
| f    | file    | 使用档案名字，必须放在命令最后，接文件名 |
| x    | extract | 从压缩包中解出文件                       |



### 八、组管理和权限管理

在linux中，每个用户必须由一个组，不能独立于组外。在linux中每个文件由所有者、所在组、其他组的概念。

- 所有组
- 所在组
- 其他组
- 改变用户所在的组

##### 1）组管理：查看所有者

一般为文件的创建者，谁创建的的该文件，谁就是该文件的所有者。

```shell
ls -ahl     
```

应用实例：创建一个police组，在创建一个tom用户，将tom放在police组，然后通过tom来创建一个ok.txt.

```shel
groupadd police
useradd -d police tom
pwd tom
touch ok.txt
```

##### 2）组管理：修改所有者

```shell
chown 用户名 文件名 
```

应用案例：使用root创建一个apple.txt,然后将其所有者修改成tom.

```shell
[root@bogon ~]# touch apple.txt
[root@bogon ~]# chown tom apple.txt
[root@bogon ~]# ls -ahl
-rw-r--r--.  1 tom  root    0 8月  13 21:15 apple.txt

```

注意：修改之后，该文件的组并没发生变化。

##### 3）组管理：修改所在组

```shell
chgrp 组名 文件名
```

应用实例：使用root用户创建文件orange.txt,看看当前文件属于哪个组，然后修改这个文件到组为police.

```shell
touch orange.txt
ls -ahl
chgrp police orange.txt
```

##### 4）组管理：其他组

除了文件的所有者和所在组之外，系统的其他用户都是文件的其他组。

- 改变用户所在组

  ```shell
  usermod -g 组名 用户名
  usermod -d 目录名 用户名         --改变该用户登录的初始目录
  ```

  应用实例：创建一个土匪组（bandit）,将tom这个用户从原来所在的police组修改到土匪组。

  ```shell
  groupadd bandit
  usermod -g bandit tom
  ```

##### 5）权限管理

1）文件的类型

ls -l 文件的信息显示：

- 第0位：文件的类型
- 第1~3位:确定所有者的拥有该文件的权限
- 第4~6位：确定所属组拥有文件的权限
- 第7~9位：确定其他用户拥有该文件的权限

```shell
-rw-r--r--. 1 tom  root      0 8月  13 21:15 apple.txt
-  普通文件
d  目录
l  软链接文件
c  字符设备【键盘、鼠标】
b  块文件【硬盘】

rw-  表示文件所有者的读写权限
r--  文件所在组的用户权限只有读的权限
r--  文件其他组的权限，只有读的权限
1    如果是文件，表示硬链接数，如果是目录，表示该目录下子目录的数量
tom  文件的所有者
police 文件的所在组
6      代表文件的大小，如果是目录统一为4096
8月  13 21:15 文件最后的修改时间
```

1）rwx权限详解

第一种：作用到文件

- r 代表可读，可看
- w 代表可写、修改，但是不代表可以删除。删除文件的前提是对该文件所在的目录有写权限。
- x 代表可执行；可以被执行；

第二种：作用到目录

- r 代表可读，可看.
- w 代表可写、修改，目录内创建+删除+重命名目录。
- x 代表可执行、可进入目录。

###### 5.1修改权限

```shell
chmod 
```

第一种：+、-、=变更权限

- u 所有者
- g 所有组
- o 其他人
- a 所有人（u、g、o的总和）

```shell
chmod u=rwx,g=rx,o=x 文件目录名
chmod o+w 文件目录名
chmod a-x 文件目录名
```

第二种：通过数字变更权限

r=4 w=2 x=1 rwx =7

```shell
chmod u=rwx,g=rw,o=x 文件目录名
chmod 751 文件名
```

###### 5.2修改文件所有者

```shell
chown newowner  file 修改文件的所有者
chown newowner:newgroup file 改变文件的所有者和所在组
-R 如果是目录，则使其他所有子文件或子目录生效
```

实例：

```
chown tom abc.txt    将home下的abc.txt的所有者改成tom
chown -R tom tom     把tom目录下的所有文件和目录的所有者改成tom
```

###### 5.3修改文件所在组

```shell
chgrp newgrep file
-R 递归下面的所有目录和文件
```

###### 5.4权限实践

### 九、croud任务调度

```shell
crontab [选项]
-e 编辑crontab定时任务
-l 查看crontab任务
-r 删除当前用户的所有crontab任务
```

任务调度是指系统在某个时间执行的特定的命令或程序。任务调度分为两类：

- 系统工作：有些工作必须周而复始的执行。如病毒扫描。
- 个别用户工作：个别用户可能需要执行某些程序。如mysql的数据备份。

案例：

```shell
1.crontab -e
2.*/1 **** ls-l/etc >> /tmp/to.txt
3.保存退出后生效，在每一分钟都会自动的调用编写的命令
```

5个占位符参数说明：

| 项目   | 含义               | 范围                 |
| ------ | ------------------ | -------------------- |
| 第一个 | 一小时中的第几分钟 | 0~59                 |
| 第二个 | 一天中的第几小时   | 0~23                 |
| 第三个 | 一月中的第几天     | 1~31                 |
| 第四个 | 一年中的第几月     | 1~12                 |
| 第五个 | 一周当中的星期几   | 0~7（0/7都市星期天） |

特殊符号说明：

| 特殊符号 | 含义                                                         |
| -------- | ------------------------------------------------------------ |
| *        | 代表任何时间。比如第一个星号，代表一小时中的每分钟都执行一次。 |
| ，       | 代表不连续的时间。比如“0 8,12,16 * * *”代表每天的8:00、12:00、16:00都执行一次。 |
| -        | 代表连续的时间范围。比如“0 5 * * 1-6”，代表在周一到周六的凌晨5点执行一次。 |
| */n      | 代表每隔多久执行一次。比如“*/10 * * * *”,代表每隔10分钟执行一次。 |

应用实例：

案例1：每隔1分钟，将当前的日期信息，追加到/tmp/mydate文件中。

```
1.先编写一个/home/mytask1.sh
date >> /tem/mydate.txt
2.给mydate.sh增加一个可执行权限
chmod 744 mydate.sh
3.crontab -e
*/1 * * * * /home/mytask1.sh
```

案例2：每隔1分钟，将当前的日期和日历信息，追加到/tmp/mycal文件中。

```shell
*/1 * * * *
```

案例3：每天凌晨2点，将mysql数据库testdb，备份到文件中。

```shell
0 2 * * *
```

### 十、分区和挂载

#### 1）分区的基本知识

- mbr分区
  - 最多支持四个主分区
  - 系统只能安装在主分区
  - 扩展分区要占一个主分区
  - mbr最大支持2TB，但拥有最好的兼容性
- gtp分区
  - 支持多个主分区（操作系统会有限制，比如windows下最多只有128个分区）
  - 最大支持18EB的大容量（EB=1024PB,PB=1024TB）
  - windows7 64位以后支持gtp

#### 2）linux分区

原理介绍：linux无论有几个分区，分给哪一个目录使用，它归根结底都只有一个根目录，一个独立且唯一的文件结构，linux中每个分区都是用来组成整个文件系统的一部分。

linux采用了一种叫“载入”的处理方法，它的整个文件系统中包含了一整套的文件和目录，且将一个分区和一个目录联系起来，这时要载入的一个分区将使它的存储空间在一个目录下获得。

- 硬盘说明

  liunx硬盘分为IDE和SCSI硬盘，目前基本是SCSI硬盘。

  对于ide硬盘，硬盘标识符为“hdx~”,其中hd表示分区所在设备的类型，x为盘号（a为基本盘，b为基本从属盘、d为辅助从属盘），~代表分区，前四个分区用1到4表示，他们时主分区和扩展分区，从5开始就是逻辑分区。例如：hda3表示第一个ide硬盘上的第三个主分区或扩展分区，hdb2表示为第二个ide硬盘上的第二哥主分区或者扩展分区。

  对于SCSI硬盘，标识为“sdx~”。SCSI硬盘用sd来表示分区所在设备的类型，其余则和ide硬盘的表示方法一致。

```shell
lsblk          查看系统的分区和挂载情况。
-f             带f，显示简要信息。
```

#### 3）添加硬盘

案例：给虚拟机增加一块硬盘，并挂载到/home/newdisk目录。

步骤：1.虚拟机添加硬盘。

 2.分区

        ```shell
fdisk /dev/sdb
n
p
1
w
​        ```

3.格式化

```shell
mkfs -t ext4 /dev/sdb1  --ext4是分区类型
```

 4.挂载

```shell
//先创建一个目录
mkdir /home/newdisk
//挂载
mount /dev/sdb1 /home/newdisk
//卸载的命令
umount 设备名称/挂载目录
```

 5.设置可以自动(永久)挂载

```shell
vim /etc/fstab      --记录分区和挂载点的情况
//在文件中增加 /dev/sdb1 /home/newdisk 
mount -a           --自动挂载

```

4）磁盘查询命令

```shell
df -h
//整个系统的磁盘情况
df -lh   --目前磁盘的使用情况，swap分区不会显示

du [选项] /目录   --查询指定目录的磁盘使用情况
-s 指定目录占用大小汇总
-h 带计量单位
-a 含文件
--max-depth=1 子目录深度
-c 列出明细的同时，增加汇总值
```

案例：

1.查询/opt的磁盘占用情况，深度为1.

```shell
du -ach --max-depth=1 /opt
```

2.统计/home 文件夹下的文件个数

```shell
ls -l /home | grep "^-" | wc -l
```

3.统计/home 文件夹目录的个数。

```shel
ls -l /home | grep "^d" | wc -l
```

4.统计/home文件夹下的目录的个数，包括子文件夹

```shell
ls -lR /home | grep "^d" | wc -l
```

5.统计/home文件夹下下文件的个数，包含子文件夹里的

```shell
ls -lR /home | grep "^-" | wc -l
```

6.以树状显示目录结构

```shell
yum install tree
tree
```

### 十一、网络配置

#### 1）查看网络IP和网关

- 虚拟网络编辑器
- 修改ip

#### 2）自动配置

linux重启之后，每次自动获取的ip地址可能不一样。不适用于做服务器。

#### 3）固定配置

- 说明

直接修改配置文件来指定ip,并可以连接到外网，编辑/etc/sysconfig/network-scripts/ifcfg-eth0(多个网卡对应多个文件).要求:将ip地址为静态的：192.168.184.130

```shell

```

### 十二、进程管理

#### 1）查看进程

```shell
ps [参数]
-a   显示所有的进程
-u   以用户的格式显示进程信息
-x   显示后台进程运行参数
ps -aux | more
ps -aux | grep 服务名     --ps -aux | grep ssh  查看ssh的进程
ps -ef | more 查看父进程

pstree [选项]  查看进程树
-p    显示进程的PID
-u    显示进程的所属用户
```

#### 2）终止进程

如果某一个进程运行到一半需要停止时，或是消耗了大量的系统资源，此时可以考虑终止进程。使用kill命令来完成此项任务。

```shell
kill [选项] 进程号
-9          强制终止
killall 进程名称
```

案例：

```shell
1.杀死某个用户的进程。
ps -aux | grep sshd
kill 4000
2.终止远程登录，在适当时重启sshd服务。
kill 3908
3.终止多个gred进程
killall gerd
4.强制杀掉一个终端
ps -aux | grep bash
kill -9 4050
```

#### 3）服务管理

服务即进程。但是它运行在后台，通常都会监听某一个端口，等待其他程序的请求，比如mysql、sshd、防火墙等，因此我们称之为守护进程。

```shell
systemctl 服务名 start | stop | restart | reload | status
```

备注：7.0之前用的时service指令。telnet ip 端口

案例

```shell
1.查看当前防火墙的状态，关闭和重启防火墙。
 systemctl status firewalld
 systemctl stop firewalld
 systemctl restart firewalld

 ls -l /etc/init.d/   查看可以启动的服务名
 netstat -ntlp        查看开启的端口号
 
 #开放端口
 #添加
firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
#重新载入
firewall-cmd --reload
```

- 运行级别

  | 运行级别 | 描述                                                    |
  | -------- | ------------------------------------------------------- |
  | 0        | 系统停机状态，系统默认级别不能为0，否则不能正常启动。   |
  | 1        | 单用户工作状态。root权限，用于系统维护，禁止远程登录。  |
  | 2        | 多用户状态，没有nfs，不支持网络。                       |
  | 3        | 有网络，登录后进入控制台命令行模式。                    |
  | 4        | 未使用。                                                |
  | 5        | 登录后进入图形GUI模式。                                 |
  | 6        | 系统关机并重启，默认运行级别不能为6，否则不能正常启动。 |

  

  服务的运行级别：开机--BIOS--/BOOT --INIT进程--运行级别--运行级别对应的服务。它在每一个运行级别中增加了一个是否自启动的选项。

  ```shell
  chkconfig --list | grep xxx           查看所有服务
  chkconfig 服务名 --list                查看某一个服务
  chkconfig --level 5 服务名 on/off	    设置自启动
  ```

#### 4）进程监控

**动态监控进程**：top与ps命令相似。他们都是用来显示正在执行的进程，不同之处是,top在执行一段时间可以更新正在运行的进程。

```
top [选项]
-d 秒数  指定top每隔几秒更新，默认是3秒在top命令的交互模式中执行。
-l top不显示任何闲置或者僵死的进程。
-p 通过指定监控进程id来仅仅监控某个进程的状态。

```

交互操作说明

```
P:以cpu的使用率排序，默认。
M:以内存的使用率排序
N:以PID排序
q:退出top
u:检索某一个用户
k:杀死某一个进程
```

案例：

```shell
top  -->  u
top  -->  k  
top -d 10 十秒更新

```

**监控网络状态**

```shell
netstat [选项]
net -anp 
-an  按一定的顺序输出
-p 
```

### 十三、RPM和YUM

#### 1）RPM管理

```shell
1.查询已经安装的rpm列表
rpm -qa|grep XX
查询是否安装firefox浏览器
rpm -qa | grep firefox
查看软件信息
rpb -qi firefox
查看软件包的文件
rpm -ql firefox
查看文件归属于哪个包
rpm -qf /etc/passwd

卸载
rpm -e rpm包名称
rpm -e firefox
rpm -e --nodeps firefox   --强制（ --nodeps）删除

安装
rpm -ivh rpm包名称 

```

案例：安装火狐浏览器

1.先找到firefox的安装包，你需要挂载我们安装centos的ios文件，然后到/media下去找rpm包。

#### 2）YUM管理

他是一个shell前端软件包管理。基于RPM包管理，能供从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包。

```shell
#查看
yum list | grep xx软件列表
#安装指定的
yum install xxx
```

案例：

安装firefox.

```shell
yum list | grep firefox
yum install firefox
```

说明：默认安装最新版本。

卸载

```shell
yum -e --nodeps 软件包名
```



### 十四、定制篇

#### 1）JDK

```shell
#1.解压
#2.配置环境变量 /etc/profile
JAVA_HOME=/opt/jdk-1.7.0_79
PATH=/opt/jdk-1.7.0_79/bin:$PATH
export JAVA_HOME PATH
#3.注销用户，使环境变量生效
运行级别为3--->logout
运行级别为5--->注销
```

#### 2）TOMCAT

```shell
#1.解压
#2.启动
 切入到apache的bin目录。
#3.开放端口
#4.常用命令
启动：./startup.sh
关闭：./shutdown.sh
带日志启动：./catalina.sh run 
查看日志：tail -f cataline.out


```

#### 3）ORACLE

参照博客：https://blog.csdn.net/qq_22260641/article/details/76182447。

问题1：/etc/security/limits.conf文件**再增加**oracle soft stack 10240。

问题2：net configuration assitant 启动/安装失败。

 解决：

```shell
# 1.修改或者增加信息
vim /etc/sysconfig/network
# NETWORKING=yes
# HOSTNAME=orcl
# 2.修改/etc/hosts,注意orcl的位置
vim /etc/hosts
#127.0.0.1   localhost localhost.localdomain localhost4 orcl localhost4.localdomain4
#::1         localhost localhost.localdomain localhost6 orcl localhost6.localdomain
# 3.hostname orcl

```

安装完成后用管理员身份登录oracle，然后启动oracle.然后启动监听。

附：oracle命令

| 命令            | 描述     |      |
| --------------- | -------- | ---- |
| netca           | 配置监听 |      |
| lstnrctl start  | 启动监听 |      |
| lstnrctl status | 监听状态 |      |
| lstnrctl stop   | 停止监听 |      |

#### 4）Nginx

参考：https://blog.csdn.net/wudinaniya/article/details/81281016

#### 5）mysql

修改密码：ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码';

### 十五、shell编程

#### 1）shell定义

​    以.sh为后缀的文件，叫做shell脚本文件。在shell文件里编写的命令叫做shell.

​    shell的种类有很多，每种shell在文件的的标识不同。linux shell用#!/bin/bash在shell文件的第一行进行标识。

```shell
#!/bin/bash
echo "hello word!"
```

通常通过***./文件名.sh***运行。为什么不是***文件名.sh***，因为直接写文件名.sh，linux回去path里去找**文件名.sh**，而只有/bin、/sbin、/usr/bin、/usr/sbin在path里，你的当前目录通常不在path里，所以会找不到命令。

用**./文件名.sh**运行,系统就会去当前目录下找。

```shell
/bin/sh echosh.sh 
/bin/php echost.php
./echosh.sh
```

#### 2）变量

分为系统变量和用户变量。

```
echo $PATH
echo $USER
```



1.定义变量：变名=值

撤销变量：unset 变量

声明静态变量:readonly 变量 ，不能unset

快速入门：

```:book:
1.定义变量A
2.撤销变量A
3.声明静态变量B，
4.把变量升级为全局变量，可供其他shell程序使用
```

**2.设置环境变量**

语法：export 变量名=变量名 -->将shell变量输出为环境变量

​           source 配置文件  -->让修改后的配置文件立即生效

​	   echo $变量名--->查询环境变量的值

**3.位置参数变量**

  	当我们使用shell脚本时，如果希望获取到命令行的参数信息，就可以使用位置参数变量。比如./myshell.sh 100 200 ,这个就是shell的命令行，可以在myshell中获取到参数信息。

  语法：

| 变量名 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| $n     | n为数字，$0代表命令本身，$1-$9代表第一到第九个参数，十以上的参数需要用大括号${10}。 |
| $*     | 这个变量代表命令行中所有的参数。$*把所有的参数看作一个整体（不包含本身$0）。 |
| $@     | 这个变量代表命令行中所有的参数。$@把所有的参数区分看待（不包含本身$0）。 |
| $#     | 代表命令行中所有参数的个数（不包含本身$0）。                 |

**4.预定义变量**

​	shell定义好的变量，可以直接在shell脚本上使用。

| 变量名 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| $$     | 当前进程的进程号                                             |
| $!     | 后台运行的最后一个进程的进程号                               |
| $?     | 最后一次执行的命令的返回状态，如果变量的值为0，证明上一个命令执行正确。如果非0，则不正确， |

#### 3) 运算符

```shell
第一种:$((n+m))
第二种：$[n=m]，推荐。	
第三种：`expr n + m` ,运算符两边有空格。乘法运算符需要转译。
例三:TEMP=`expr 3 + 2`;
RESULT=`expr $TEMP /* 4`;

```

#### 4）判断语句

判断条件

```shell
基本语法：[ condition ] （condition前后有空格）
#非空返回true,可使用$?验证（0为true,>1为false）

```

 判断种类：

```shell
1）两个整数比较(= 字符串比较)
 -lt -le -eq -gt -ge -ne
2）按文件判断比较
-r -w -x
3）按文件类型判断
-f -e -d (-d文件存在并且是一个常规文件)
```

应用实例：

```shell
#"ok"是否等于“ok”
[ ok = ok ]
#23是否大于等于22
[ 23 -ge 22 ] 
#/root/Install.log目录中的文件是否存在。
[ -e /root/Install.log ]
```





### 十六、补充

#### 1）selinux

selinux是美国国家安全局（NSA）对于强制访问控制的实现，是linux历史上最杰出的新安全子系统。

```shell
#查看selinux的状态
gentenforce 
#告警，不启用
setenforce 0
#启用
setenforce 1
#永久生效，修改SELINUX=disabled
vim /etc/selinux/config
```















