---
date:
    created: 2024-10-29
categories:
    - Linux
tags:
    - Linux
---

# 专题5-Ubuntu用户管理

简单介绍下Ubuntu的用户管理
<!-- more -->

## 1 引言

本文主要介绍了Ubuntu系统中用户管理的基本概念、操作方法以及用户组的管理。首先，文章解释了root用户和普通用户的区别，并强调了root用户的高权限特性及其使用sudo命令执行特定操作的方式。接着，文章详细描述了如何切换到root用户、添加和删除用户，以及如何处理用户删除异常情况。此外，还介绍了用户组的概念、查看用户所属组信息的方法、查看系统所有用户组的信息、添加和删除用户组，以及如何将用户添加到或从用户组中移除。最后，文章通过具体命令示例，展示了如何在CLI环境中进行这些操作。

 

## 2 root 用户

### 2.1 root用户介绍

- 在Ubuntu中，root用户是系统的超级用户，拥有对系统的完全控制权限。与普通用户相比，`root`用户可以执行系统级别的操作，例如安装软件、修改系统配置、管理用户权限等。
- 一般用户在Ubuntu系统中只拥有有限的权限，不能对系统做出影响性的更改。普通用户可以使用sudo（superuserdo） 命令来以root权限执行特定的命令，但这需要输入密码并且只有在配置了sudo权限的情况下才能够执行。
- root用户与普通用户的主要区别在于权限的不同。root用户可以执行系统级别的操作，而普通用户只能执行自己拥有权限的操作。由于root用户权限过高，在日常使用中，建议尽量避免使用root用户登录系统，以免误操作导致系统出现问题。

 

### 2.2切换到 root 用户

（1）设置root用户密码。Ubuntu安装过程中，只会让设置登录用户和登录密码，并没有设置root用户密码的过程，因此 Ubuntu安装完成之后默认是没有root账户登录权限的。Ubuntu系统启动会自动生成一个root用户的密码，是随机的。但是用户可以主动修改root用户密码，从而实现root账户登录。

在 Ubuntu 系统中, root 用户没有设置默认密码。首先需要为root创建密码

```shell
sudo passwd root
```

根据系统提示，输入root用户密码

![](../../../PageImage/Pasted%20image%2020241029102712.png)


（2） 将当前用户临时切换到 root 用户。

```shell
su - root
```

> su：switch user

输入root密码，这样就可以使用root用户了。

![](../../../PageImage/Pasted%20image%2020241029102738.png)

> 注意：提示符变成了root@xxx

（3）退出当前的 shell 环境或终端

```shell
exit
```

![](../../../PageImage/Pasted%20image%2020241029103311.png)

退出当前的 shell 环境：结束当前Shell进程并返回到上一级的Shell环境或用户桌面

可以类比为打开了多个程序窗口, 当你关闭一个窗口时, 并没有关闭电脑或者操作系统, 而是回到了之前的工作空间

> shell 是一个命令行解释器, 负责接收和解析用户通过终端输入的命令。
>
> 每当用户在终端中输入一条命令, shell 会立即将其  "翻译"  成操作系统可以理解的指令。
>
> 终端是一个提供命令输入和输出环境的程序, 可以把它看作是一个窗口, 让用户可以看到操作系统的反馈。
>
> 而 shell 则是这个窗口中的工具, 帮助用户向操作系统发出指令。

 

（4）`su root` 和 `su - root` 在使用上的区别

- `su root`

在使用`su root`命令时，不会加载`root`用户的环境变量。这意味着您将在当前用户的环境下切换到`root`用户身份，**不会改变当前工作目录和环境设置**。

您仍然会保留当前用户的权限和环境设置，只是切换到root用户的身份。

```shell
su root
pwd
```

![](../../../PageImage/Pasted%20image%2020241029103508.png)

执行完pwd命令后，显示的当前目录是/home/caicloudcat

- `su - root`

使用`su - root`命令时，会加载root用户的完整环境变量。这意味着您将切换到root用户的身份，并使用root用户的环境设置。

当使用`su - root`时，会将当前工作目录更改为root用户的主目录（/root），并加载root用户的shell配置文件（例如.bashrc）。

```shell
su - root
pwd
```

![](../../../PageImage/Pasted%20image%2020241029103815.png)

可以看到执行pwd命令后，显示的当前目录是 /root



通常情况下，推荐使用su - root来切换到root用户身份，因为这样可以确保您以root用户的完整环境执行命令，并避免由于环境变量不一致而导致的问题。然而，如果您只是需要在当前用户身份下暂时执行某些需要root权限的命令，那么使用su root可能更为方便。

## 3 添加、删除用户

### 3.1 添加用户

添加用户需要超级用户的权限，我们可以切换到root用户获得权限，或者在命令前加上sudo，这里我们先切换到root用户。

```shell
su - root
```

在桌面环境中打开/home文件夹，便于我们观察。

![](../../../PageImage/Pasted%20image%2020241029104558.png)

![](../../../PageImage/Pasted%20image%2020241029104651.png)

![](../../../PageImage/Pasted%20image%2020241029104743.png)

![](../../../PageImage/Pasted%20image%2020241029104809.png)

可以看到/home中目前只有一个caicloudcat的文件夹，因为此刻我的系统除了root用户以外，只有一个用户caicloudcat，这个用户是我安装ubuntu的时候创建的默认用户。

 

回到CLI环境，输入下列命令创建`student1`用户：

```shell
adduser student1
```

![](../../../PageImage/Pasted%20image%2020241029105732.png)

输入`student1`用户的密码

![](../../../PageImage/Pasted%20image%2020241029105748.png)

接下来是输入用户信息，我都是直接敲回车，用默认配置，最后输入"y"确认

![](../../../PageImage/Pasted%20image%2020241029105813.png)

在桌面的文件管理器中，可以看到系统在`/home`下为`student1`用户创建了用户主目录`/home/student1`

> 文件夹上打个红叉叉是因为我们还没有获得打开该目录的权限

![](../../../PageImage/Pasted%20image%2020241029105842.png)

双击`student1`目录，输入授权信息

![](../../../PageImage/Pasted%20image%2020241029110933.png)

可以进去`/home/student1`目录（默认是个空文件夹）

![](../../../PageImage/Pasted%20image%2020241029111006.png)

当然，你也可以在CLI环境中输入下列命令查看该系统上所有已创建用户的主目录 

```shell
ls /home
```

![](../../../PageImage/Pasted%20image%2020241029111036.png)

同样可以看到 /home下有两个目录 student1 和 caicloudcat



### 3.2 删除用户

回到CLI环境，输入下列命令删除student1用户：

```shell
deluser student1
```

![](../../../PageImage/Pasted%20image%2020241029111559.png)

在桌面环境下，可以看到 /home/student1用户主目录依然存在（用ls /home命令可以看到相同的结果）：

![](../../../PageImage/Pasted%20image%2020241029111658.png)

这是因为只执行deluser命令时，不会删除用户相关的文件，你可以选择手工删除或者保留这些文件。如果要删除student1用户主目录，执行下列命令：

```shell
rm -r /home/student1
```

![](../../../PageImage/Pasted%20image%2020241029111755.png)

> 但是桌面环境下的 /home/studnet1文件夹还在，这是因为桌面没有刷新：
>
> 可以退出重进就发现其已经被删除


如果你希望删除用户时，同时删除用户相关的主目录，可以执行以下命令：

```shell
adduser student2  
deluser --remove-home studnet2
```

![](../../../PageImage/Pasted%20image%2020241029112331.png)

这样在删除用户时，同时删除了用户主目录。



### 3.3 删除用户异常情况的处理

在删除用户时，有时候会提示用户被进程占用，大概是下面的提示：

报错 userdel: user luna is currently used by process 4857

这说明用户被进程4857占用了，后面我们会专门讲ubuntu进程管理的内容。这里先简单了解一下。

输入下面命令，显示当前终端会话中运行的进程的详细信息

```shell
ps -f
```

![](../../../PageImage/Pasted%20image%2020241029112622.png)

- `UID (User ID)` 进程用户ID
- `PID (Process ID) `进程ID
- `PPID (Parent Process ID)` 父进程ID
- `C(CPU)` 进程占用 CPU 的百分比
- `STIME (Start Time)` 进程启动的具体时间
- `TTY (Teletypewriter)` 与进程交互的终端设备
- `TIME` 启动进程花费的 CPU 时间
- `CMD` 启动进程的命令

输入下面命令，显示系统中所有正在运行的进程的详细信息（系统进程很多）

```shell
ps -ef
```

![](../../../PageImage/Pasted%20image%2020241029142504.png)

输入下面命令， 强制结束进程

```shell
kill -9 4857
```

> -9 表示发送 SIGKILL[signal kill] 信号给进程 id 为 4857 的进程
>
> SIGKILL 信号是一种强制停止进程的信号



## 4 用户组管理

### 4.1 用户组基本概念

在 Ubuntu 系统中，用户组（==Groups==）是用于管理用户权限的一种方式。每个用户可以属于一个或多个用户组，而每个用户组可以拥有对系统资源的不同访问权限。这样做的目的是为了简化权限管理，并确保系统的安全性和可管理性。

例如，一个新生入学后，成为了普通本科生，同时担任了班级班长，并且加入了校学生会宣传部成为了宣传干事，我们让这个学生加入普通本科生组、班干部组、校学生会宣传部组，这个学生便会继承这三个组的权限。另外一位新老师担任学生辅导员，并负责管理校学生会宣传部，我们让这个老师加入教师组、辅导员组、校学生会宣传部组，这个老师便会继承这三个组的权限。这种基于用户组的权限管理模式在使用上会方便很多。

### 4.2 查看用户的所属组信息

输入下面命令，显示当前用户的所属组信息：

```shell
groups
```

![](../../../PageImage/Pasted%20image%2020241029142719.png)

可以看到，caicloudcat这个用户属于9个用户组，这些用户组的介绍如下：

- caicloudcat: 组名为 caicloudcat的用户组（caicloudcat用户隶属于和自己同名用户组）。ubuntu在创建用户时，需要为新建用户指定一用户组，如果不指定其用户所属的工作组，则系统会自动会生成一个与用户名同名的工作组。
- `adm(Administrator)` : 管理员用户组, 具有系统管理权限
- `cdrom(CD-ROM) `: 光盘用户组, 具有读取光盘的权限
- `sudo(Super User Do)` : 超级用户组, 具有执行系统管理任务的权限
- `dip(Device Interface)` : 接口用户组, 具有配置网络接口的权限
- `plugdev(Plug-in Device)` : 设备插件用户组, 具有管理设备插件(如声卡、显卡等)的权限
- `lpadmin(Local Printer Administration) `: 打印机管理用户组, 具有管理打印机的权限
- `users`

> lxd（Linux Containers eXecution Driver）：Ubuntu LXD是一个工具，用于在Ubuntu系统上创建和管理容器。LXD用户组是用于管理LXD功能的用户组。
>
> sambashare(Samba share) : 在Linux系统中，Samba是一种广泛使用的文件共享服务，它允许不同操作系统之间共享文件和打印机。Samba share是该服务的用户组。

输入下面命令，显示指定用户的所属组信息：

```shell
groups caicloudcat
groups root
```

![](../../../PageImage/Pasted%20image%2020241029143029.png)

root 用户隶属于 root 组, root 组被赋予了最高的权限, 允许其成员访问系统中的所有资源。

### 4.3 查看系统所有用户组的信息

在Ubuntu系统中，**/etc**目录下，有三个文件：passwd、shadow、group，这三个配置文件用于系统帐号管理，都是文本文件，可用vim等文本编辑器或者cat命令打开。

- `/etc/passwd` ：用于存放用户帐号信息
- `/etc/shadow` ：用于存放每个用户加密的密码
- `/etc/group` ：用于存放用户的组信息

 

==/etc==目录说明：

“/etc”目录是指 etcetera（意为附加物）缩写，存放系统w的各种配置文件。这些配置文件用于设置各种系统和应用程序的参数。在这个目录下，可以找到一些重要的配置文件，如“/etc/passwd”（存储用户信息）、“/etc/fstab”（存储文件系统的挂载信息）等。

输入下面命令，显示系统所有的用户组信息：`cat /etc/group`

![](../../../PageImage/Pasted%20image%2020241029144039.png)

`/etc/group `文件的每行格式是 `group_name:x:GID:group members`

- `group_name `表示用户组的名称
- `x` 表示密码占位符, 密码是存储在`/etc/shadow`文件中
- `GID` 表示组`ID(GID)`, 用于唯一标识用户组
- `group members` 表示该用户组的成员, 每个成员用逗号分隔    

例如：

![](../../../PageImage/Pasted%20image%2020241029144100.png)

adm组，x 是密码占位符，组ID是4，有两个组成员syslog和caicloudcat。

输入下面命令，列出包含caicloudcat字符串的用户组的信息：

```shell
grep caicloudcat /etc/group
```

![](../../../PageImage/Pasted%20image%2020241029144253.png)

- `adm:x:4:syslog,caicloudcat` 	[表示名为`adm`的组, 组密码是x, 组ID是4, 组成员包括syslog和caicloudcat]
- `cdrom:x:24:caicloudcat`      [表示名为`cdrom`的组, 组密码是x, 组ID是24, 组成员包括caicloudcat]
- `sudo:x:27:caicloudcat`     [表示名为`sudo`的组, 组密码是x, 组ID是27, 组成员包括caicloudcat]
- `dip:x:30:caicloudcat`      [表示名为`dip`的组, 组密码是x, 组ID是30, 组成员包括caicloudcat]
- `plugdev:x:46:caicloudcat`     [表示名为`plugdev`的组, 组密码是x, 组ID是46, 组成员包括caicloudcat]
- `lpadmin:x:122:caicloudcat`     [表示名为`lpadmin`的组, 组密码是x, 组ID是122, 组成员包括caicloudcat]
- `caicloudcat:x:1000:`     [表示名为caicloudcat的组, 组密码是x, 组ID是1000, 没有其他组成员]

输入下面命令，查看用户caicloudcat的用户ID和组ID：`id caicloudcat`

![](../../../PageImage/Pasted%20image%2020241029192144.png)

```shell
uid=1000(caicloudcat) gid=1000(caicloudcat) groups=1000(caicloudcat) ,4(adm) ,24(cdrom) ,27 (sudo) ,30 (dip) ,46 (
lugdev) , 100 (users) , 114 (lpadmin)
```

这说明`caicloudcat`的uid（user id）是1000，gid（group id）是1000，所在的组id分别是为1000、4、24、27、30、46、100、114。

### 4.4 添加用户组

输入下面命令，创建一个用户`student1`：

```shell
su - root 
adduser student1
```

![](../../../PageImage/Pasted%20image%2020241029193443.png)

输入下面命令，创建一个用户组 students：

```shell
groupadd students
```

输入下面命令，查看结果：

```shell
grep students /etc/group
```

![](../../../PageImage/Pasted%20image%2020241029193714.png)

可以看到 `students` 用户组创建成功，gid是 1002。

输入下面命令，将 studnet1 用户添加到 students 用户组中，

```shell
groups student1
usermod -a -G students student1
groups student1
```

![](../../../PageImage/Pasted%20image%2020241029194030.png)

说明：

- -a 表示以追加方式（append）将用户`student1`添加到` students `组中, 不影响其原有所属组

  若省略了 -a, 用户student1将从其当前组中删除,并被添加到名为students的新组中

- -G students 表示将用户添加到名为 students 的组中

从`groups`命令可以看出，原来`student1`仅在同名的`student1`组中，执行`usermod`命令后，属于`student1`和`students`两个用户组了。

输入下面命令，将 studnet1 用户从 students 用户组中删除：

```shell
deluser student1 students
```

![](../../../PageImage/Pasted%20image%2020241029194422.png)

可以看到 student1 仅在同名的student1组中了。

输入下面命令，删除students 用户组：

```shell
groupdel students
```

![](../../../PageImage/Pasted%20image%2020241029194601.png)

可以看到students用户组已经被删除了。

输入下面命令，尝试删除 student1 用户组，

```shell
groupdel student1
```

![](../../../PageImage/Pasted%20image%2020241029194944.png)

可以看到删除studnet1用户组失败了，因为 student1 用户组是用户 student1 的主组（primary group）。