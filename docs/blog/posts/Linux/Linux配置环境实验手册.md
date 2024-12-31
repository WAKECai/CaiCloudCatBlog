---
date:
    created: 2024-10-04
    updated: 2024-10-08
readtime: 30
categories:
    - Linux
tags:
    - Linux
    - 配置环境
---
# Linux配置环境实验手册

Linux配置环境实验手册，进行安装VMware Workstation以及安装Ubuntu。
<!-- more -->

## 实验手册1：安装 VMware Workstation

VMware Workstation之前已经安装完成，这里不再赘述，安装也比较简单

![](../../../PageImage/Pasted%20image%2020240924112724.png)

以下具体的操作步骤：（重新安装）

首先先进去并登录进入[页面](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Workstation+Pro)

![](../../../PageImage/Pasted%20image%2020240924113052.png)

![](../../../PageImage/Pasted%20image%2020240924120915.png)

## 实验手册2：在虚拟机中安装Ubuntu

### 1.安装Linux发行版的安装包

官网：<https://cn.ubuntu.com/>

注：Ubuntu也有很多版本

!!! not "桌面版和服务器版的区别"
    Ubuntu Desktop是新手或刚开始使用Linux系统用户的完美选择，因为它简洁直观的用户界面和默认应用程序可以帮助用户入门。

    Ubuntu Server是为服务器环境而构建的，它是一个轻量级和简约的版本，它剥离了任何GUI应用程序和元素，以提高运行生产级应用程序的速度和性能。它可以用作Web服务器、文件服务器、开发服务器和DNS服务器，当然还包括其它一些应用。

    如果对Linux很熟悉的话，可以下Ubuntu的服务器版（Server），如果不是特别熟悉Linux命令，可以使用Desktop版本。两者的功能是一样的。

    我选择使用Desktop版本，因为很多Linux命令有一段时间不用就会忘记了，有时候可以用GUI（Graphical User Interface，简称 GUI，又称图形用户接口）来救急。

??? info "tips"
    Ubuntu 长期支持（LTS）与临时发布版本

    Ubuntu版本号由年份和月份组成，例如，Ubuntu 23.10代表2023年10月发布的版本。
    
    Ubuntu发布版本分为 长期支持版本（LTS）和 临时发布版本（Interim Release）。
    
    <mark>长期支持版本（LTS）</mark>
    
    LTS版本每两年发布一次，通常在四月发布。LTS版本被认为是“企业级”发布版本，也是使用最广泛的版本。大约95%的Ubuntu安装都是LTS版本。LTS版本提供长达5年的标准安全维护，涵盖“Main”仓库中的所有软件包。
    
    对于希望延长安全维护的用户，Ubuntu Pro订阅提供了扩展安全维护（ESM），覆盖“Main”和“Universe”仓库中的软件包，维护期长达10年。此外，用户还可以选择额外的电话和工单支持，这些支持同样覆盖ESM中的软件包。
    
    在Ubuntu Pro订阅的基础上，用户可以选择额外的Legacy支持，将安全维护和支持延长至12年。
    
    <mark>临时发布版本</mark>
    
    在LTS版本之间，Canonical每六个月发布一次临时版本，例如最新的23.10版本。临时发布版本是生产质量的版本，支持期为9个月，为用户提供了足够的更新时间。然而，这些版本不具备LTS版本的长期承诺。

在下载的时候，出现了一个小意外，当我点击下载链接时，出现了“Not Found”错误

![](../../../PageImage/Pasted%20image%2020240924185114.png)

这时候可以选择阿里的镜像网站下载Ubuntu：<https://mirrors.aliyun.com/oldubuntu-releases/releases/?spm=a2c6h.25603864.0.0.63826f0frd44zC>

我选择的是24.04版本

![](../../../PageImage/Pasted%20image%2020240924185400.png)

### 2.使用虚拟机安装Ubuntu

#### 自定义安装配置

首先创建一个新的虚拟机

![](../../../PageImage/Pasted%20image%2020240924185727.png)

安装模式选择“自定义安装“

硬件兼容性用默认配置：

![](../../../PageImage/Pasted%20image%2020240924185834.png)

选择光盘镜像所在的位置，就是第一步骤下载的ISO文件
![](../../../PageImage/Pasted%20image%2020240924190017.png)

填写相关信息：

全名：caicloudcat

用户名：caicloudcat

密码：123456

![](../../../PageImage/Pasted%20image%2020240924190125.png)

命名虚拟机

注意：如果你安装在C盘，要保证你的C盘有足够的容量（默认需要20G容量），如果C盘容量不够，你可以自己换一个盘安装。

![](../../../PageImage/Pasted%20image%2020240924190354.png)

处理器配置，设置2颗处理器，每个处理器的内核数是2

内存设置，设置4G内存

网络类型（重点）主要使用两种

桥接原理图：参考 <https://mango-chen.blog.csdn.net/article/details/130779901>
![](../../../PageImage/Pasted%20image%2020240924190550.png)

NAT原理图：参考 <https://blog.csdn.net/qq_42700289/article/details/130779927>

![](../../../PageImage/Pasted%20image%2020240924190614.png)

> 备注：网络模式我更喜欢用桥接模式，这样以后可以把虚拟机当成主系统所在的网络中的一台服务器来使用，外部的其他主机可以直接访问虚拟服务器，但是存在一个问题，虚拟机的ip地址会随着主机移动而变化（我们的笔记本会到处带来带去的，网络环境经常变化，所以ip地址经常在变）。
>
> 由于暂时不需要外部设备访问虚拟服务器，而且桥接模式的ip地址变动太麻烦了，所以我使用==NAT连接方式==（如果是固定的服务器，我更喜欢用桥接模式）。

![](../../../PageImage/Pasted%20image%2020240924190722.png)

选择控制器类型，采用默认设置

![](../../../PageImage/Pasted%20image%2020240924190810.png)

选择磁盘类型，使用默认设置
![](../../../PageImage/Pasted%20image%2020240924190831.png)

选择磁盘，使用默认设置

![](../../../PageImage/Pasted%20image%2020240924190919.png)

分配磁盘容量，使用默认设置（20G）

![](../../../PageImage/Pasted%20image%2020240924191124.png)

指定磁盘文件，使用默认配置

![](../../../PageImage/Pasted%20image%2020240924191229.png)

完成设置，开始安装

![](../../../PageImage/Pasted%20image%2020240924191259.png)

然后虚拟机就自动开启了，在虚拟机中继续安装Ubuntu

#### 虚拟机中继续安装

出现ubuntu桌面后，要点击一下（有个空白页不点就会停在那里）。

先选择语言，有很多语言版本（包括中文版），但是很多Linux服务器版只有英文版，所以这边我们还是选英文版吧。

![](../../../PageImage/Pasted%20image%2020240924191707.png)

![](../../../PageImage/Pasted%20image%2020240924191736.png)

继续选择“Accessibility”选项，用默认

继续选择键盘布局，用默认

选择联网方式，可以选”wired……”（有线网络）或者“WIFI……”（WIFI），有什么选什么。如果只有“Do not connect to the internet”，可能是前面安装的问题（如360关闭了权限），最好重头再试一遍（从安装vmware开始）。
![](../../../PageImage/Pasted%20image%2020240924191900.png)

接下来是更新界面，先跳过去吧（有可能会直接跳到下一步骤）

接下来是问是安装还是试用，选安装

接下来选用交互模式安装还是自动化安装，选交互模式

![](../../../PageImage/Pasted%20image%2020240924192103.png)

接下来选安装哪些app，用默认模式

接下来问要不要装推荐软件，先不选

接下来问我们如果安装ubuntu

输入信息，填上你的用户名和密码

![](../../../PageImage/Pasted%20image%2020240924192404.png)
选择位置（时区），用默认Shanghai

最后，选择install开始安装
![](../../../PageImage/Pasted%20image%2020240924192451.png)

安装完成后要重启一下

![](../../../PageImage/Pasted%20image%2020240924193656.png)

需要输入密码：
![](../../../PageImage/Pasted%20image%2020240924194446.png)

成功打开Ubuntu的桌面

![](../../../PageImage/Pasted%20image%2020240924195706.png)

是否要升级为ubuntu Pro，先选skip

是否分享数据，选择否

结束安装

进入桌面后，可以试一下火狐，看上网行不行
![](../../../PageImage/Pasted%20image%2020240924200020.png)

上网没问题

安装完成

> 注意：如果直接用ubuntu服务器版本，是没有GUI图形界面的，我们用的桌面版，可以使用图形界面，这样入门容易点，不过我们后面主要讲解都是shell命令的使用，就是一行一行输入命令的模式。

克隆ubuntu

我们成功安装了ubuntu，因为以后的大数据环境很多都是集群模式，会有很多服务器，这里我们把当前安装好的ubuntu保存起来，以后在模拟集群环境时，可以在vmware中直接克隆多台服务器，这样就不用一台一台安装了。

先关闭ubuntu

![](../../../PageImage/Pasted%20image%2020240924200857.png)

关机后，在vmware中用鼠标右键选择这台虚拟机，选择“管理”，再选择“克隆”。

出现克隆虚拟机向导：

![](../../../PageImage/Pasted%20image%2020240924200936.png)

选择“克隆自”-“虚拟机中的当前状态”

![](../../../PageImage/Pasted%20image%2020240924200945.png)

选择“创建完整克隆”：

![](../../../PageImage/Pasted%20image%2020240924201100.png)

输入新的虚拟机名称，我填的是“Linux实训”

![](../../../PageImage/Pasted%20image%2020240924201146.png)

克隆完成

vmware左边出现了两台虚拟机，以后上课就用“Linux实训”这台虚拟机

![](../../../PageImage/Pasted%20image%2020240924201221.png)

#### 虚拟机删除

1、选中要删除的虚拟机操作系统，单击右键，选择“管理”选项

2、然后在选择“从磁盘中删除”选项即可删除该虚拟机操作系统
