---
date: 
    created: 2024-10-14
reatime: 35
categories:
    - Linux
tags:
    - Linux
---

# 专题2-Linux基本文件操作

Linux基本文件操作讲解。
<!-- more -->

## 1 引言

Linux系统中的文件操作是日常管理和维护系统的基础。下面是一些基本的文件操作命令，这些命令在大多数Linux发行版中都是可用的。

## 2 Linux Shell和桌面

在Windows环境下，我们已经习惯了图形化可视桌面操作环境。

![](../../../PageImage/Pasted%20image%2020241008105549.png)

实际上，微软最开始做的操作系统是DOS（Disk Operating System，磁盘操作系统），现在Windows中保留的”命令提示符“模式可以看成内嵌的DOS。

![](../../../PageImage/Pasted%20image%2020241008105652.png)

Linux提供了两种操作环境： 

**方式一：**

在Linux环境下，类似于DOS/命令提示符 的环境称之为 **命令行界面** （**CLI**，command-line interface）。命令行界面是一种文本界面，用户可以通过输入命令来完成操作。

Linux 系统默认提供一个命令行终端（terminal），用户可以使用它来进行命令行操作。命令行界面常用于服务器系统或远程操作，因为它通常比图形界面更快、更简单、更稳定。

更多的时候，我们把CLI称为 **Shell**，Shell俗称壳（用来区别于核）。Linux命令是通过Shell解释器执行的，Shell环境是Linux操作系统提供的一种命令行解释器，用于解析和执行用户输入的命令。

常见的Shell环境包括Bash（Bourne Again SHell）、Korn shell、C shell等。不同的Shell环境对于命令的解释和执行方式有所不同，但基本的命令语法和功能是相同的。
![](../../../PageImage/Pasted%20image%2020241008110234.png)

**方式二：**

图形用户界面（Graphical User Interface，GUI）：图形用户界面是一种图形化的界面，它使用图标、菜单和鼠标来完成操作。大多数 Linux 发行版都包含一个图形化的桌面环境，如 Gnome、KDE、Xfce 等，用户可以使用这些桌面环境来进行操作。

我们常常把Linux GUI成为 **桌面环境**，**GNOME** 是 Ubuntu 的默认桌面环境。
![](../../../PageImage/Pasted%20image%2020241008110305.png)

在Linux环境下，需要重点学习和掌握的是 **Shell命令**，因为服务器一般都不安装桌面环境。

（1）没必要装图形桌面，因为我们企业服务都是在后台运行的，不涉及图形操作，即使装图形桌面的，要么是小白，要么这个软件需要图形化操作。

（2）降低资源开销。图形桌面呢，会涉及到很多的额外组件，这些组件在运用过程中呢，都会消耗额外的资源 

（3）稳定性高。通用桌面相比于纯命令行界面，它出现问题的概率就比较大，纯命令上界面更简单，更轻量级。

（4）第四，降低安全性。图形桌面它包含了很多的组件，包括浏览器呃，邮件、客户端、文件管理器，这些组件呢，就会增加系统的攻击面。

## 3 文件操作命令

### pwd

`pwd (print working directory)`：显示当前工作目录

![](../../../PageImage/Pasted%20image%2020241008110719.png)

说明：我直接从用户主目录中打开terminal窗口，用pwd命令显示当前工作目录为`/home/caicloudcat`，`~`代表的是当前用户的主目录，可以看出我的主目录就是`/home/caicloudcat`

> 注意：你的主目录可能是其他的文件夹，后面的命令要根据你自己的Linux环境适当修改。

***

### ls

`ls (list)`：列出当前目录下的文件和子目录

- `ls`
- `ls -l` 按照长格式`(long format)`显示文件信息

![](../../../PageImage/Pasted%20image%2020241008111226.png)

***

### cd

`cd (change directory)`：切换目录

```shell
cd ~/Desktop
cd ~
cd ..
cd ../
```

![](../../../PageImage/Pasted%20image%2020241008112144.png)

??? not "相对路径与绝对路径"
    相对路径是以当前目录"./" 为基准的路径, 是从当前目录到目标文件或目录的路径. 如`./web/test.txt`表示当前目录下的 web 目录中的`test.txt`文件
    
    相对路径中 "./" 表示当前目录, "../" 表示上一级目录
    
    绝对路径是相对于系统 根目录"/" 的完整路径. 如`/home/david/web`
    
    说明：这里所说的绝对路径就是我们以前说的根相对路径。
    
    练习：绝对路径、相对路径和根相对路径的相互转换。

***

### mkdir

`mkdir (make directory)`：创建一个新目录

创建单个目录

```shell
mkdir web
```

创建多个目录

```shell
mkdir web test
```

创建多级目录

>  [p:parents 父级目录] -p表示创建指定的目录,并自动创建其中所需的所有缺少的父级目录

```shell
mkdir -p web/test
```

![](../../../PageImage/Pasted%20image%2020241008113340.png)

***

### touch

`touch`：创建空文件

- 创建单个空文件

```shell
touch web.txt
```

- 创建多个空文件

```shell
touch demo.txt test.txt
```

![](../../../PageImage/Pasted%20image%2020241008113547.png)

***

### echo

`echo`：打印输出文本

```shell
echo "Hello World!"
```

![](../../../PageImage/Pasted%20image%2020241008130337.png)

使用`>>`向文件中添加一行文字 

>  `>> web.txt `将打印输出的文本追加到 `web.txt `文件末尾，若文件不存在，则会创建该文件 

```shell
echo "CaiCloudCat" >> web.txt
```

> \> 符号是重定向输出，会覆盖已有的文件
>
> \>> 则会保留原来文件的内容, 在文件末尾追加内容

![](../../../PageImage/Pasted%20image%2020241008133358.png)
![](../../../PageImage/Pasted%20image%2020241008133433.png)

>  我们还没有学习怎么使用vim编辑器，所以先使用可视化方式打开。

***

### cat

`cat (concatenate)`显示文件内容

```shell
cat web.txt
```

>  cat可以简单的显示文件内容，但没有编辑功能，CLI环境下可以使用vim编辑器编辑文件内容。

![](../../../PageImage/Pasted%20image%2020241008133820.png)

***

### tail

`tail `从文件**末尾**显示指定数量的行

>  默认显示文件的最后 10 行

```shell
tail web.txt
```

![](../../../PageImage/Pasted%20image%2020241008133841.png)

显示文件的最后 1 行

```shell
tail -n 1 web.txt
```

>  说明：这个命令用的少，了解一下即可。

![](../../../PageImage/Pasted%20image%2020241008133902.png)

***

### head

`head `从文件开头显示指定数量的行

> 默认显示文件的前 10 行

```shell
head web.txt
```

![](../../../PageImage/Pasted%20image%2020241008133915.png)

***

### copy

`cp (copy)`：复制

- 将文件复制到另一个目录中

```shell
cp web.txt /home/caicloucat/Desktop/test
```

![](../../../PageImage/Pasted%20image%2020241008134135.png)

![](../../../PageImage/Pasted%20image%2020241008134251.png)

说明：这个命令是把当前文件夹的`web.txt`拷贝到`/home/caicloucat/Desktop/test`目录下，你要确保当前目录下有这个文件。

```shell
cp ~/Desktop/web/demo.txt ~/Desktop/test
```

![](../../../PageImage/Pasted%20image%2020241008134350.png)

![](../../../PageImage/Pasted%20image%2020241008134401.png)


- 将文件复制到另一个目录中并重命名

```shell
cp /home/caicloucat/Desktop/web/web.txt /home/caicloucat/Desktop/web/newWeb.txt
```

![](../../../PageImage/Pasted%20image%2020241008134450.png)

![](../../../PageImage/Pasted%20image%2020241008134515.png)


- 将目录复制到另一个目录中

  > `[r:recursive 递归]` `-r`表示复制整个目录树的内容

```shell
cp -r  /home/caicloucat/Desktop/web/ /home/caicloucat/Desktop/a/
```

![](../../../PageImage/Pasted%20image%2020241008134604.png)

![](../../../PageImage/Pasted%20image%2020241008134632.png)

说明：web目录和其中包含的所有内容被拷贝到`/home/caicloucat/Desktop/a/`下面，成为了一个子目录。



***

### mv

`mv (move)`：重命名或移动文件

#### 文件

- 重命名文件

```shell
mv web.txt web1.txt
```

![](../../../PageImage/Pasted%20image%2020241008134729.png)

![](../../../PageImage/Pasted%20image%2020241008134758.png)

- 移动文件

```shell
mv web1.txt ~/Desktop/test
```

![](../../../PageImage/Pasted%20image%2020241008134835.png)

![](../../../PageImage/Pasted%20image%2020241008134854.png)

- 移动文件并重命名

```shell
mv newWeb.txt ~/Desktop/test/test2.txt
```

![](../../../PageImage/Pasted%20image%2020241008134936.png)

![](../../../PageImage/Pasted%20image%2020241008135002.png)

#### 目录

- 重命名目录

```shell
cd ..
mv web newWeb
```

![](../../../PageImage/Pasted%20image%2020241008135033.png)
![](../../../PageImage/Pasted%20image%2020241008135054.png)

- 移动目录

```shell
mv newWeb ~/Desktop/test
```

![](../../../PageImage/Pasted%20image%2020241008135125.png)
![](../../../PageImage/Pasted%20image%2020241008135139.png)

移动目录并重命名

```shell
cd test
mv newWeb ~/Desktop/newnewWeb
```

![](../../../PageImage/Pasted%20image%2020241008135216.png)

![](../../../PageImage/Pasted%20image%2020241008135231.png)

***

### rm

`rm (remove)`：删除文件或目录

- 删除单个文件

```shell
cd ../newnewWeb
rm test.txt
```

![](../../../PageImage/Pasted%20image%2020241008135355.png)

![](../../../PageImage/Pasted%20image%2020241008135415.png)

- 删除多个文件

```shell
cd ../test
rm web.txt web1.txt
```

![](../../../PageImage/Pasted%20image%2020241008135450.png)

![](../../../PageImage/Pasted%20image%2020241008135501.png)

- 删除目录

>  `[r:recursive 递归]` -r表示删除此文件夹和其子文件夹中的所有文件和目录

```shell
cd ../newnewWeb
rm -r test
```

![](../../../PageImage/Pasted%20image%2020241008135537.png)

![](../../../PageImage/Pasted%20image%2020241008135551.png)