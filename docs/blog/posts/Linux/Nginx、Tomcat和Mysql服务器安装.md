---
date:
    created: 2024-12-01
    updated: 2024-12-04
draft: True
readtime: 120
categories:
    - Linxu
tags:
    - Linux
    - 服务器
    - Nginx
    - Tomcat
    - MySQL

---
# 在Linux中安装Nginx、Tomcat和Mysql服务器

本文章将在Linux操作系统中安装Nginx、Tomcat和MySQL服务器，采用虚拟机Linux进行操作，以Ubuntu24.04为例进行安装。

<!-- more -->

## Nginx

如果我们需要上传一个网站到服务器，需要安装HTTP Server（也称为Web服务器）。常用的Web服务器有nginx和Apache HTTP Server，当然我们常用的Tomcat也集成了Web服务的功能。

Nginx 是开源的轻量级 Web 服务器、反向代理服务器，以及负载均衡器和 HTTP 缓存器。其特点是高并发，高性能和低内存。

Nginx最初由Igor Sysoev为俄罗斯访问量第二的Rambler.ru站点开发，其将源代码以类BSD许可证的形式发布，因它的稳定性、丰富的功能集、简单的配置文件和低系统资源的消耗而闻名。Nginx可以在大多数Unix、Linux OS上编译运行，并有Windows移植版。


### 安装Nginx

安装Nginx有几种常见的方法

方法一：通过APT包管理器安装，即使用`apt-get`命令安装


方法二：从源码包安装



#### 通过 apt-get 安装 Nginx

使用以下命令进行安装：

```shell
sudo apt-get update
sudo apt-get install nginx
```

![](../../../PageImage/Pasted%20image%2020241202200004.png)

#### 从源码包安装 Nginx

##### 下载并解压源代码包

首先在本机去官网下载nginx包，安装稳定包

上传nginx到Linux系统自定义下的目录下（上传可以使用Xftp），并将其解压。

上面的一些初始步骤在之前的文章[专题8-压缩和解压缩文件](./压缩和解压缩文件.md)详细讲解过。

如果你要在Ubuntu中进行下载源代码包，则使用：

```shell
wget http://nginx.org/download/nginx-<version>.tar.gz
```
我安装的是稳定版本（stable version）是 `1.26.2`，所以命令应该是：

```shell
wget http://nginx.org/download/nginx-1.26.2.tar.gz
```
##### 安装所需依赖包

Nginx是基于C语言开发的，所以安装nginx前需要安装C语言编译环境，HTTP rewrite 模块要求安装PCRE库，SSL模块要求OpenSSL库，执行以下命令来安装所需的依赖包

```shell
sudo apt-get install gcc libpcre3-dev zlib1g-dev openssl libssl-dev
```

那么如何查看已经安装的依赖包呢？

使用`dpkg`命令，该命令会列出所有已安装的软件包

```shell
dpkg -l
```
但是内容过长， 不容易查看，因此可以使用`grep`来筛选特定的软件包：

```bash
dpkg -l | grep <package-name>
```


##### 编译安装 Nginx

首先进入解压缩完后的nginx目录，我这里是`nginx-1.26.2`：

```bash
cd nginx-1.26.2
```

进入nginx-1.26.2目录后，即可执行configure脚本生成编译配置文件Makefie：

```bash
./configure --prefix=/usr/local/nginx
```

![](../../../PageImage/Pasted%20image%2020241203185647.png)

这是一个非常简易的配置安装，你可以配置你需要的module，完整的文档可参考[Building nginx from Sources](https://nginx.org/en/docs/configure.html)。


!!! note "注意"
	`--prefix`是配置安装的路径，如果不配置该选项，安装后可执行文件默认放在`/usr/local/bin`，库文件默认放在`/usr/local/lib`，配置文件默认放在`/usr/local/etc`，其它的资源文件放在`/usr/local/share`，比较凌乱。上述命令配置`--prefix`，可以把所有资源文件放在`/usr/local/nginx`的路径中，不会杂乱。

稍微讲解上述的一些内容解释：

```
–prefix 指定nginx安装目录

–pid-path 指向nginx的pid

–lock-path 锁定安装文件，防止被恶意篡改或误操作

–error-log 错误日志

–http-log-path http日志

–with-http_gzip_static_module 启用gzip模块，在线实时压缩输出数据流

–http-client-body-temp-path 设定客户端请求的临时目录

–http-proxy-temp-path 设定http代理临时目录

–http-fastcgi-temp-path 设定fastcgi临时目录

–http-uwsgi-temp-path 设定uwsgi临时目录

–http-scgi-temp-path 设定scgi临时目录
```



**Makefile** 是一个用于自动化编译和构建项目的文件，通常用于管理源代码的编译过程。它包含了一组规则，指示 `make` 工具如何从源文件生成目标文件（如可执行文件或库文件）。Makefile 使得项目的构建过程更加高效、可重复和自动化，特别是在大型项目中。

一个基本的 Makefile 包括以下部分：

1. **目标（Target）**：  
    目标是 Makefile 中需要生成的文件。通常是一个可执行文件、一个库文件或中间文件（例如 `.o` 文件）。目标通常出现在每行的最前面。
    
2. **依赖（Dependencies）**：  
    依赖是目标所依赖的文件。只有当依赖的文件发生变化时，目标才会重新构建。依赖关系描述了源文件和目标文件之间的关系。
    
3. **规则（Rule）**：  
    规则描述了如何从依赖生成目标。通常包括一个命令，这个命令会在目标需要更新时执行。规则通常由命令行组成，命令前面会有一个 tab（制表符）字符。

接下来进行编译并安装：

```bash
make # 编译源码
sudo make install # 安装Nginx
```

如果没有安装`make`，则使用下面的命令进行安装：

```bash
sudo apt update
sudo apt isstall make
```

安装完成后，使用`whereis`命令查看是否安装成功：
```shell
whereis nginx
```
![](../../../PageImage/Pasted%20image%2020241203191349.png)
出现`/usr/local/nginx`即完成安装，其他的是之前使用apt-get方法安装Nginx留存的。

或者可以使用下面的命令，检查Nginx的版本：

```bash
nginx -V
```

![](../../../PageImage/Pasted%20image%2020241203192428.png)

这是`usr/local/nginx`目录的详细内容：

![](../../../PageImage/Pasted%20image%2020241203191628.png)

进入 nginx 目录下的 sbin 目录，执行命令：

```bash
sudo ./nginx # 启动
sudo ./nginx -s stop # 停止
sudo ./nginx -s reload # 重新加载
```

但在运行上面的代码时候，出现该问题：

![](../../../PageImage/Pasted%20image%2020241203194222.png)

原因是该端口已经有服务，因为我之前使用apt包安装Nginx后该服务还在启动中。

先将apt包安装的Nginx服务停掉，再试一遍：

```shell
sudo sytemctl stop nginx
sudo lsof -i:80
sudo /usr/local/nginx/sbin/nginx
sudo lsof -i:80
```

![](../../../PageImage/Pasted%20image%2020241203195129.png)
可以发现启动成功。


### 配置其他现有 Web 服务器

如果您的 Ubuntu 服务器上安装了其他 Web 服务器（例如 Apache），请在安装 Nginx 之前卸载它们。这将避免任何冲突或端口绑定问题。

```shell
sudo apt-get remove apache2
```
或者，如果您想与 Apache 一起运行 Nginx，您可以选择使用 Nginx 作为 Apache 的反向代理。此配置允许 Nginx 处理传入请求并将其转发给 Apache 进行处理。此设置可以提供两个 Web 服务器的优点。

### 测试Nginx

使用下面的命令来检查服务是否正在运行：

```shell
systemctl status nginx
```

![](../../../PageImage/Pasted%20image%2020241202200515.png)

从上面的图片可以确认服务已经成功启动了。不过，最好的方式是实际从Nginx 要求一个网页。

你可以通过访问预设的Nginx 登陆页面，来确认软体运行正常。只需前往你伺服器的IP 地址，可以通过`ifconfig`或者`ip address`来查看IP地址。

将它输入到你浏览器的地址栏中：

```
http://your_serve_ip
```

然后就会看到预设的Nginx 登陆页面：

![](../../../PageImage/Pasted%20image%2020241202202024.png)
提示：如果启动 Nginx 服务时出现错误，很有可能是 80 端口已被使用。Nginx 默认使用端口 80 进行 HTTP 流量。如果另一个服务已经使用了80端口，Nginx将无法启动。要检查80端口是否被使用，可以运行以下命令：

```shell
sudo lsof -i :80
```

![](../../../PageImage/Pasted%20image%2020241202204557.png)

这里看到是Nginx在运行服务，如果另一个服务使用端口 80，您可以停止该服务或将 Nginx 配置为使用其他端口。

### 配置防火墙

如果您已在系统上启用 UFW 防火墙，请确保对其进行适当配置，以允许 Nginx 使用的端口上的传入流量。Nginx 使用的默认端口是 HTTP 的 80 和 HTTPS 的 443。

首先使用`sudo ufw status verbose`来查看防火墙状态（包括规则详细信息）

![](../../../PageImage/Pasted%20image%2020241202205543.png)

您可以运行以下命令来允许 Nginx 的流量。

```shell
sudo ufw allow 'Nginx HTTP'
sudo ufw allow 'Nginx HTTPS'
```

![](../../../PageImage/Pasted%20image%2020241202205413.png)
再查看防火墙状态，可以看到如下：
![](../../../PageImage/Pasted%20image%2020241202205600.png)

> UFW（Uncomplicated Firewall）是一个简单的防火墙管理工具，主要用于简化 Linux 系统上的 iptables 配置。它提供了一个简单的命令行接口，使得设置防火墙规则变得更加直观和易于管理。UFW 适用于大多数 Linux 发行版，如 Ubuntu 和 Debian。

### 管理Nginx进程（Nginx Processing）

要停止你的网页伺服器，输入以下指令：

```shell
sudo systemctl stop nginx
```

如果网页伺服器停止了，要重新启动它，请输入以下指令：

```shell
sudo systemctl start nginx
```

如果要先停止再重新启动服务，请输入以下指令：

```shell
sudo systemctl restart nginx
```

如果你只是在进行设定更改，通常Nginx 可以在不断开连线的情况下重新载入。要这么做，输入以下指令：

```shell
sudo systemctl reload nginx
```

预设情况下，Nginx 设定为在伺服器启动时 **自动启动** 。如果你不希望这样，可以通过输入以下指令来停用这个功能：

```shell
sudo systemctl disable nginx
```

若要重新启用服务在开机时自动启动，请输入以下指令：

```shell
sudo systemctl enable nginx
```

那么为什么会有这些快捷指令？它是Nginx安装后自动配置的吗？其实是通过配置Systemd File 服务单元文件，来管理Nginx服务。

### 配置 Systemd File

通过`apt-get`来安装Nginx，它会自动在`/lib/systemd/system`目录下给你创建一个`nginx.service`。

![](../../../PageImage/Pasted%20image%2020241203195916.png)

我们来看看它长什么样子：

```nginx title="nginx.service" linenums="1"
# Stop dance for nginx
# =======================
#
# ExecStop sends SIGQUIT (graceful stop) to the nginx process.
# If, after 5s (--retry QUIT/5) nginx is still running, systemd takes control
# and sends SIGTERM (fast shutdown) to the main process.
# After another 5s (TimeoutStopSec=5), and if nginx is alive, systemd sends
# SIGKILL to all the remaining processes in the process group (KillMode=mixed).
#
# nginx signals reference doc:
# http://nginx.org/en/docs/control.html
#
[Unit]
# Description提供了服务的简短描述
Description=A high performance web server and a reverse proxy server
# Documentation提供了该服务的相关文档：指向Nginx的手册页
Documentation=man:nginx(8)
# After定义了该服务的执行顺序, 他将在 network-online.target、remote-fs.target、
# nss-lookup.target 完成后执行, 也就是在网络配置、远程文件系统和 NSS（名称服务切换）准备好之后启动
After=network-online.target remote-fs.target nss-lookup.target
# Nginx 服务希望 network-online.target 处于激活状态，但它不是强制要求。
# 也就是, 即使 network-online.target 没有完全完成, Nginx 仍会尝试启动。
Wants=network-online.target

[Service]
# 表示 Nginx 是通过派生子进程来运行的。
Type=forking
# PIDFile 指定了 Nginx 主进程的 PID 文件路径，该文件包含 Nginx 主进程的 PID
# systemd 会通过这个文件来管理 Nginx 的启动、停止等操作。
PIDFile=/run/nginx.pid 
# ExecStartPre 命令在实际启动 Nginx 之前执行，用于检查配置文件是否正确。
# -t 用于测试配置，-q 用于减少输出，
# -g 'daemon on; master_process on;' 用于确保 Nginx 在正确的模式下运行。
ExecStartPre=/usr/sbin/nginx -t -q -g 'daemon on; master_process on;'
# 启动 Nginx 的实际命令
ExecStart=/usr/sbin/nginx -g 'daemon on; master_process on;'
# 该命令用于重新加载 Nginx 配置文件，而不需要停止 Nginx 服务。
ExecReload=/usr/sbin/nginx -g 'daemon on; master_process on;' -s reload
# ExecStop 用于停止 Nginx 服务。它向 Nginx 主进程发送 `QUIT` 信号，以优雅的方式关闭 Nginx。
# --retry QUIT/5 表示如果在 5 秒内 Nginx 进程没有退出，start-stop-daemon 会强制退出。
# - 符号表示即使命令执行失败，也不会导致服务的停止失败。
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid
# TimeoutStopSec 指定了在发送 QUIT 信号后，等待 Nginx 停止的最大时间。
# 如果 Nginx 在 5 秒内没有停止，systemd 将强制停止 Nginx。
TimeoutStopSec=5
# KillMode 设置为 mixed，表示在停止服务时，systemd 会先发送 QUIT 信号给主进程（优雅停机）
# 然后，如果主进程在 TimeoutStopSec 时间内没有终止，systemd 会发送 SIGTERM 信号
# 最后发送 SIGKILL 强制终止所有相关进程。
KillMode=mixed

[Install]
# 指定了当系统进入 multi-user.target 时，Nginx 服务应该被自动启动。
WantedBy=multi-user.target

```

该配置文件为 Nginx 提供了一个完善的启动、停止和重载机制，确保服务能够在系统启动时自动管理。

如果你是使用源代码包进行安装，则可以自已创建来管理Nginx。

可以使用下面的命令创建：

```shell
sudo vim /lib/systemd/system/nginx.service
```

然后将相应的配置写入，这里不再详细介绍。

最后，重新加载：

```shell
sudo systemctl daemon-reload
```

### 从本地上传网站

我们接下来将从本地（Windows系统）上传一个网站到nginx服务器，并测试。

#### 配置文件知识

首先我们用apt包管理器下载的Nginx来查看一些基础的配置文件

进入`/etc/nginx`目录下：

![](../../../PageImage/Pasted%20image%2020241203213005.png)

进入`sites-available`目录下，可以看到有一个`default`文件：

![](../../../PageImage/Pasted%20image%2020241203213109.png)

我们用`vim`来看看`default`文件的内容：

```nginx title="default" linenums="1"
##
# You should look at the following URL's in order to grasp a solid understanding
# of Nginx configuration files in order to fully unleash the power of Nginx.
# 你应该查看以下 URL，以便对 Nginx 配置文件有深入的了解，从而充分释放 Nginx 的强大功能。
# https://www.nginx.com/resources/wiki/start/
# https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/
# https://wiki.debian.org/Nginx/DirectoryStructure
#
# In most cases, administrators will remove this file from sites-enabled/ and
# leave it as reference inside of sites-available where it will continue to be
# updated by the nginx packaging team.
# 在大多数情况下，管理员会从 sites-enabled/ 中删除此文件，
# 并将其作为 sites-available 内的参考，以便 nginx 打包团队继续更新它。
# This file will automatically load configuration files provided by other
# applications, such as Drupal or Wordpress. These applications will be made
# available underneath a path with that package name, such as /drupal8.
# 此文件将自动加载其他应用程序（例如 Drupal 或 Wordpress）提供的配置文件。
# 这些应用程序将在具有该包名称的路径下提供，例如 /drupal8。
# Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.
##

# Default server configuration
#
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        # SSL configuration
        #
        # listen 443 ssl default_server;
        # listen [::]:443 ssl default_server;
        #
        # Note: You should disable gzip for SSL traffic.
        # See: https://bugs.debian.org/773332
        #
        # Read up on ssl_ciphers to ensure a secure configuration.
        # See: https://bugs.debian.org/765782
        #
        # Self signed certs generated by the ssl-cert package
        # Don't use them in a production server!
        #
	    # include snippets/snakeoil.conf;

        root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
				try_files $url $uri/ =404;
		}
        # pass PHP scripts to FastCGI server
        #
        #location ~ \.php$ {
        #       include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
        #       fastcgi_pass unix:/run/php/php7.4-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #       deny all;
        #}
}
# Virtual Host configuration for example.com
#
# You can move that to a different file under sites-available/ and symlink that
# to sites-enabled/ to enable it.
#
#server {
#       listen 80;
#       listen [::]:80;
#
#       server_name example.com;
#
#       root /var/www/example.com;
#       index index.html;
#
#       location / {
#               try_files $uri $uri/ =404;
#       }
#}
```

接下来讲解一些上述内容：

`server`块

Nginx 的 `server` 块用来定义一个虚拟主机（vhost），这意味着它负责处理来自客户端的请求。每个 `server` 块都能绑定一个 IP 地址和端口，可以有多个 `server` 块来处理不同的域名或 IP。

```nginx
server {
	listen 80 default_server;
	listen [::]:80 default_server;
}
```
这行代码表示：
- `listen 80`：该服务器监听 IPv4 的 80 端口（HTTP 默认端口）。
- `listen [::]:80`：该服务器监听 IPv6 的 80 端口。
- `default_server`：这个配置会将该服务器设置为 **默认服务器** ，当请求没有匹配到任何 `server_name` 时会使用这个服务器。

SSL配置

```nginx
# SSL configuration 
# listen 443 ssl default_server; 
# listen [::]:443 ssl default_server; 
# include snippets/snakeoil.conf;
```

这部分是 SSL 配置，但它被注释掉了，表示此服务器没有启用 HTTPS 配置。如果启用了，你需要提供 SSL 证书文件以及相关配置。`443` 是 HTTPS 的默认端口。

root 指令

```nginx
root /var/www/html;
```

这行定义了网站的根目录。Nginx 会从这个路径查找文件并返回给客户端。当用户访问网站时，Nginx 会寻找相应的文件（如 `index.html`）并返回给用户。

index 指令

```nginx
index index.html index.htm index.nginx-debian.html;
```

这指定了默认的文件列表，当访问根目录（`/`）时，Nginx 会优先返回这些文件。

如果用户访问网站的根目录而不指定文件名，Nginx 会依次查找 `index.html`、`index.htm` 和 `index.nginx-debian.html`。

server_name 指令

```nginx
server_name _;
```

`server_name` 指令用来定义此服务器响应的域名。在这里，`_` 表示默认匹配任何请求，这在没有配置特定域名时会生效。通常你会把它替换为你自己的域名，例如 `example.com`。

location 块

```nginx
location / {
    try_files $url $uri/ =404;
}
```

`location` 块用于匹配请求的 URI，并为其提供相应的处理规则。在这里：

- `try_files $url $uri/ =404`：Nginx 会首先检查请求的 URL 是否与某个文件匹配，如果匹配则返回该文件。如果没有匹配到文件，接着会检查是否有匹配的目录。如果都没有匹配，最后会返回 404 错误。


PHP 配置

```nginx
#location ~ \.php$ {
#    include snippets/fastcgi-php.conf;
#    fastcgi_pass unix:/run/php/php7.4-fpm.sock;
#    fastcgi_pass 127.0.0.1:9000;
#}
```

这部分被注释掉了，它是用来处理 PHP 请求的。如果你需要处理 PHP 文件（如 `.php` 文件），则需要配置 FastCGI 与 PHP-FPM。

.htaccess 文件的限制

```nginx
#location ~ /\.ht {
#    deny all;
#}
```

这部分配置用来阻止访问 `.htaccess` 文件。如果你使用 Apache 的 `.htaccess` 文件，Nginx 会拒绝对其的访问，因为 Nginx 并不使用 `.htaccess` 文件，而是通过配置文件直接进行访问控制。

在 `sites-available` 目录中有许多虚拟主机配置文件，通常会通过符号链接（symlink）将需要启用的配置链接到 `sites-enabled` 目录。


#### apt包管理器安装的Nginx

首先来到其默认的网页管理目录下：

```bash
cd /var/www/html
ls -l
```

![](../../../PageImage/Pasted%20image%2020241204002742.png)

可以看到该目录下有一个默认的`index.nginx-debian.html`网页，用`vim`查看该文件：

![](../../../PageImage/Pasted%20image%2020241204002912.png)

可以看到就是之前的页面的html源代码。

我们可以将自己本地的测试网站上传到该目录下，但是因为权限不够而无法上传。

`www`和`html`目录的权限都是`rwxr-xr-x`。

比较简单的方法就是修改该目录的权限：

```bash
sudo chmod -R 777 /var/www/
```

执行命令后在传输，即可成功

![](../../../PageImage/Pasted%20image%2020241204003524.png)

在网站中输入`http://your_server_ip/testpage.html`查看是否正确显示，在这里我的是`http://192.168.64.10/testpage.html`

![](../../../PageImage/Pasted%20image%2020241204003940.png)


#### 源码包安装的Nginx

其步骤核心跟上面的大致相同，首先关闭来自于上面的Nginx服务，并启动当前的Nginx服务。

```bash
sudo systemctl stop nginx
sudo /usr/local/nginx/sbin/nginx
```

接着去安装Nginx的目录下，即`/usr/local/nginx`下。

![](../../../PageImage/Pasted%20image%2020241204103519.png)

跟之前的一样，将`html`目录权限进行修改，以及上传我的测试网页。

```bash
sudo chmod -R 777 /usr/local/nginx/html
```

![](../../../PageImage/Pasted%20image%2020241204104447.png)

![](../../../PageImage/Pasted%20image%2020241204104640.png)

接着来检查一下，输入地址`http://192.168.64.10/testpage.html`

![](../../../PageImage/Pasted%20image%2020241204104821.png)

可以看到已经有页面显示，完成上传~

### 参考

[源代码安装Nginx（nginx-1.22.1)](https://blog.csdn.net/puchiliu/article/details/136609216)

[Nginx 源码编译安装与运行](https://xie.infoq.cn/article/bf9b7b36f916cc70ecb6b45db)

[Ubuntu源码安装Nginx详解](https://cloud.baidu.com/article/3210948)

[如何在 Ubuntu 上安装和使用 Nginx](https://blog.gaomeluo.com/archives/UbuntuNginx/)

Very interesting article： [How to Install Nginx from Source on Ubuntu](https://facsiaginsa.com/nginx/how-to-install-nginx-from-source)

[基于nginx上传一个简单的Html网页到服务器，并进行访问](https://blog.csdn.net/sunandstarws/article/details/104741143)

[How to Deploy a Simple Website with Nginx: A Comically Easy Guide](https://dev.to/starcc/how-to-deploy-a-simple-website-with-nginx-a-comically-easy-guide-202g)

[Install an NGINX web server on Ubuntu and create a website!](https://medium.com/@terminalsandcoffee/create-a-website-with-nginx-on-ubuntu-7e80a3d17d09)


## Tomcat


## MySQL

