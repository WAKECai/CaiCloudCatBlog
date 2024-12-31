---
date:
    created: 2024-12-23
    updated: 2024-12-23
draft: true
categories:
    - Server
    - Nginx
tags:
    - Nginx
    - 服务器
---

# Nginx学习笔记01

记录下Nginx学习笔记，方便以后复习。

<!-- more -->

## mime.types

`mime.types`是一个用于标识不同文件类型及其对应的MIME（Multipurpose Internet Mail Extensions）类型的配置文件，在Web服务器和客户端之间的文件传输及处理中起着关键作用，以下是对其的详细介绍：

### 基本概念

- **MIME类型**：是一种标准化的方式，用于标识文档、文件或字节流的性质和格式。它由两部分组成，即类型和子类型，中间用`/`分隔，如`text/html`表示HTML文档，`image/jpeg`表示JPEG图像。MIME类型使得客户端（如浏览器）能够正确地处理和显示接收到的文件内容。
- **mime.types文件**：是一个包含了大量文件扩展名与MIME类型对应关系的文本文件。Web服务器通过读取这个文件，根据请求文件的扩展名来确定其MIME类型，然后在HTTP响应头中设置`Content-Type`字段，告诉客户端该文件的类型，以便客户端能够正确地处理和显示文件。

### 常见的MIME类型与文件扩展名对应关系

| MIME类型 | 描述 | 常见文件扩展名 |
| ---- | ---- | ---- |
| `text/plain` | 纯文本文件 |.txt、.log、.conf等 |
| `text/html` | HTML文档 |.html、.htm |
| `text/css` | CSS样式表 |.css |
| `text/javascript` | JavaScript脚本 |.js |
| `image/jpeg` | JPEG图像 |.jpg、.jpeg |
| `image/png` | PNG图像 |.png |
| `image/gif` | GIF图像 |.gif |
| `application/pdf` | PDF文档 |.pdf |
| `application/zip` | ZIP压缩文件 |.zip |
| `application/json` | JSON数据格式 |.json |

### 在不同服务器中的作用

- **Apache服务器**：在Apache中，`mime.types`文件通常位于服务器的配置目录下。当服务器接收到一个文件请求时，它会查找该文件的扩展名在`mime.types`文件中的对应MIME类型，并将其添加到HTTP响应头的`Content-Type`字段中。如果在`mime.types`文件中找不到对应的类型，服务器可能会使用默认的MIME类型或根据文件的内容进行猜测。
- **Nginx服务器**：Nginx也使用`mime.types`文件来确定文件的MIME类型。与Apache类似，它会在处理文件请求时查找该文件扩展名对应的MIME类型，并在响应头中设置`Content-Type`。Nginx的`mime.types`文件通常位于其安装目录下的`conf`文件夹中。

### 实际应用

- **浏览器渲染**：当浏览器请求一个网页资源时，服务器会根据`mime.types`文件设置的MIME类型来告知浏览器如何处理该资源。例如，如果是`text/html`类型，浏览器会将其解析为HTML页面并进行渲染；如果是`image/jpeg`类型，浏览器会将其显示为图片。
- **文件下载**：在下载文件时，浏览器会根据文件的MIME类型来决定如何处理。如果是`application/zip`类型，浏览器通常会提示用户保存文件或直接在本地解压；如果是`text/plain`类型，浏览器可能会直接在新窗口中打开显示文本内容。
- **内容协商**：一些网站可能会根据客户端的能力和偏好提供不同格式的内容。通过`mime.types`文件和HTTP的`Accept`头信息，服务器可以进行内容协商，为客户端提供最合适的内容格式。

## nginx.conf

nginx.conf 是 Nginx 的主配置文件，一般位于 `/etc/nginx/nginx.conf` 目录下。这个文件包含了 Nginx 的总体配置，包括全局配置、虚拟主机配置、日志配置等。

其大致结构如下：

```bash

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

简易的nginx.conf文件结构。

```bash
worker_processes  1;

events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;


    sendfile        on;

    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost; # 域名、主机名


        location / {
            root   html;
            index  index.html index.htm;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

    }

}
```

1.`default_type`：`default_type application/octet-stream;`

- 当 Nginx 无法从 mime.types 文件中找到对应的 MIME 类型时，就会使用这个默认值

- application/octet-stream 表示二进制文件

- 当浏览器收到这种类型的响应时，通常会选择下载文件而不是直接显示

2.`sendfile`：`sendfile on;`

- 启用 sendfile 系统调用来传输文件

- 工作原理：
  - 传统方式：硬盘 → 内核缓冲区 → 用户缓冲区 → socket 缓冲区
  - sendfile：硬盘 → 内核缓冲区 → socket 缓冲区（省略了用户缓冲区）

- 优点：
  - 减少数据拷贝次数，提高传输效率
  - 减少内存使用，降低系统负载

3.`server`：`server { ... }`

- 定义一个虚拟主机 vhost
- 包含 listen、server_name、location 等配置

## 虚拟主机与域名解析

### 域名、DNS、IP地址的关系

### 三者之间的关系示例

用户访问过程：

1. 用户输入：`www.baidu.com`
2. DNS解析过程：`www.baidu.com ----DNS服务器----> 14.215.177.39`
3. 浏览器访问：`14.215.177.39`对应的服务器

域名（Domain Name）

- 域名是一个便于人类记忆的网站地址，比如 `www.baidu.com`
- 它由几个部分组成：
  - 顶级域名（.com）
  - 二级域名（baidu）
  - 三级域名（www）
- 作用：提供一个容易记忆的网站访问方式，避免直接使用IP地址

DNS（Domain Name System）

- DNS是"域名系统"的缩写，主要功能是域名与IP地址的相互转换
- 工作流程：
  1. 用户在浏览器输入域名
  2. 本地DNS客户端首先查找本地缓存
  3. 如果没有，则向DNS服务器发起查询请求
  4. DNS服务器返回对应的IP地址
  5. 本地DNS客户端缓存该结果
  6. 浏览器使用获得的IP地址访问目标服务器

IP地址（Internet Protocol Address）

- IP地址是计算机网络中设备的唯一标识
- 分为IPv4（如：14.215.177.39）和IPv6
- 作用：
  - 标识网络中的设备
  - 实现设备之间的通信
  - 确定数据包的传输路径

### 浏览器、Nginx与http协议

#### 工作流程

1. **浏览器发起请求**
   - 用户在浏览器输入URL（如 `http://example.com`）
   - 浏览器通过DNS解析获取服务器IP地址
   - 浏览器创建HTTP请求报文

2. **Nginx处理请求**
   - Nginx监听指定端口（默认80）接收HTTP请求
   - 根据请求头中的Host字段确定由哪个虚拟主机处理
   - 按照location配置规则匹配请求的URI
   - 处理请求（静态文件、反向代理等）

3. **HTTP协议通信**
   - 请求报文格式：

     ```nginx
     请求行：GET /index.html HTTP/1.1
     请求头：Host: example.com
            User-Agent: Mozilla/5.0
            ...
     请求体：(POST请求才有)
     ```

   - 响应报文格式：

     ```nginx
     状态行：HTTP/1.1 200 OK
     响应头：Content-Type: text/html
            Content-Length: 1234
            ...
     响应体：<html>...</html>
     ```

#### Nginx的角色

1. **Web服务器**
   - 处理静态资源请求（HTML、图片、CSS等）
   - 配置缓存控制
   - 访问控制和安全防护

2. **反向代理**
   - 转发请求到后端服务器
   - 负载均衡
   - SSL终止

3. **HTTP协议实现**
   - 支持HTTP/1.0、HTTP/1.1
   - 支持HTTPS（HTTP + SSL/TLS）
   - 支持HTTP/2
   - 处理HTTP请求头和响应头
   - 管理连接（keep-alive、超时等）

### 虚拟主机原理

#### 什么是虚拟主机

虚拟主机（Virtual Host）是在一台物理服务器上运行多个网站的技术。通过虚拟主机，可以：

- 在同一个Nginx服务器上托管多个网站
- 为不同域名提供不同的内容
- 有效利用服务器资源

#### 虚拟主机的工作原理

1. **基于域名的虚拟主机**
   - 客户端请求中包含Host头部
   - Nginx根据Host头部匹配server_name
   - 转发到对应的虚拟主机配置

2. **基于端口的虚拟主机**
   - 不同的网站使用不同的端口
   - 通过listen指令配置端口监听
   - 访问时需要指定端口号

### 域名解析与泛域名解析实战

Windows下配置域名解析：

1. 打开`C:\Windows\System32\drivers\etc\hosts`文件
2. 添加域名解析，如：`127.0.0.1 www.baidu.com`，或者虚拟机的IP地址即`192.168.1.100 test.com`
3. 保存文件

但是通常情况下，Windows系统下hosts文件权限限制，无法直接编辑，需要使用管理员权限访问。
或者提高Users权限，然后使用记事本编辑。
也可以复制hosts文件到桌面，然后使用记事本编辑，再替换原文件。

## Nginx虚拟主机域名配置

详见：[Nginx](../Linux/Nginx.md) 中的[创建Nginx虚拟主机(Virtual Host)](../Linux/Nginx.md#创建Nginx虚拟主机Virtual-Host)

## ServerName匹配规则

- 完整匹配
- 通配符匹配
- 通配符结束匹配
- 正则匹配

## 域名解析相关项目实战技术架构

### 多用户域名

### 短网址

### HttpDns

## 学习参考资料

[Nginx入门必须懂3大功能配置 - Web服务器/反向代理/负载均衡](https://www.bilibili.com/video/BV1TZ421b7SD)
