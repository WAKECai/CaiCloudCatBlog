---
date:
    created: 2024-12-17

categories:
    - Linux

tags:
    - Linux
---


# 专题12-使用 systemctl 命令

了解使用 systemctl 命令控制 nginx 服务、MySQL服务等服务的方法。
<!-- more -->

## systemctl 基础知识

### systemctl 介绍

systemctl 是一个用于控制系统和服务管理器的命令行工具，通常在基于 systemd 的 Linux 发行版中使用。

systemd 是一个系统和服务管理器，提供了一个统一的框架来启动系统、管理服务以及运行守护进程。

在Windows中，有一个类似的”服务“管理器，点击桌面左下角的Windows图标或按下键盘上的Win键，打开“开始”菜单，在开始菜单的搜索栏中键入“服务”，然后在搜索结果中选择“服务”应用程序。

![](../../../PageImage/Pasted%20image%2020241217103301.png)


### 常用的 systemctl 命令及其功能

（1）启动服务

```shell
sudo systemctl start <service_name>
```

例如，启动 Apache 服务：

```shell
sudo systemctl start apache2
```

（2）停止服务

```shell
sudo systemctl stop <service_name>
```

例如，停止 Apache 服务：

```shell
sudo systemctl stop apache2
```

（3）重启服务

```shell
sudo systemctl restart <service_name>
```

例如，重启 Apache 服务：

```shell
sudo systemctl restart apache2
```

（4）重新加载服务配置

```shell
sudo systemctl reload <service_name>
```

例如，重新加载 Apache 配置：

```shell
sudo systemctl reload apache2
```

（5）检查服务是否已设置为开机自动启动

```shell
sudo systemctl is-enabled <service_name>
```

假设你要检查 nginx 服务是否已设置为开机自动启动，你可以运行：

```shell
sudo systemctl is-enabled nginx
```

这个命令会返回以下几种结果之一：

- enabled：表示服务已设置为开机自动启动。
- disabled：表示服务未设置为开机自动启动。
- masked：表示服务已被禁用，并且无法启动。
- static：表示服务是静态的，不能被启用或禁用。
- unknown：表示服务不存在或状态无法确定。

（6）启用服务（开机自启）

```shell
sudo systemctl enable <service_name>
```

例如，设置 Apache 开机自启：

```shell
sudo systemctl enable apache2
```

（7）禁用服务（开机不自启）

```shell
sudo systemctl disable <service_name>
```

例如，禁用 Apache 开机自启：

```shell
sudo systemctl disable apache2
```

（8）检查服务状态

```shell
sudo systemctl status <service_name>
```

例如，检查 Apache 服务状态：

```shell
sudo systemctl status apache2
```

（9）列出所有服务

```shell
systemctl list-units --type=service
```

（10）查看服务的日志

```shell
journalctl -u <service_name>
```

例如，查看 Apache 的日志：

```shell
journalctl -u apache2
```

（11）立即停止所有服务

```shell
sudo systemctl halt
```

（12）重启系统

```shell
sudo systemctl reboot
```

（13）关闭系统

```shell
sudo systemctl poweroff
```

（14）列出服务的依赖关系

```shell
systemctl list-dependencies <service_name>
```

（15）将服务及其依赖项一起隔离

```shell
systemctl isolate <target>
```

例如，切换到多用户模式（不带图形界面）：

```shell
sudo systemctl isolate multi-user.target
```

这些命令提供了对服务和系统管理的广泛控制，使得系统管理员能够轻松地管理系统运行的各种方面。


## 用 systemctl 命令管理 Nginx 和 MySQL 服务

用 systemctl命令管理Nginx和MySQL服务，例如查看服务状态，把服务设置为开机自启动等。

这些命令在之前的教程中已经讲述的差不多了，这里简单的讲解一下。

```shell
sudo systemctl status nginx
sudo systemctl status mysql
```

![](../../../PageImage/Pasted%20image%2020241217104242.png)

![](../../../PageImage/Pasted%20image%2020241217104320.png)

检查一下两者的服务是否自启动：

```bash
caicloudcat@caicloudcat-VMware-Virtual-Platform:~$ sudo systemctl is-enabled nginx
enabled
caicloudcat@caicloudcat-VMware-Virtual-Platform:~$ sudo systemctl is-enabled mysql
enabled
caicloudcat@caicloudcat-VMware-Virtual-Platform:~$ 
```

因为我的已经设置过，所以两者都是`enabled`，如果没有设置过，可以执行下面的命令：

```shell
sudo systemctl enable nginx
sudo systemctl enable mysql
```

如果是自己用源码安装Nginx，则可以通过配置Systemd File之后，就可以使用`systemctl`来操作，具体操作在之前的[Nginx、Tomcat和Mysql服务器安装](./Nginx、Tomcat和Mysql服务器安装.md)中的配置Systemd File。
