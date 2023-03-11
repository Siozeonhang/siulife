---
title: "搭建临时邮箱 forsaken-mail (Docker)"
datePublished: Mon Apr 18 2022 05:46:16 GMT+0000 (Coordinated Universal Time)
cuid: clf3jo2mk000t09mk3d51d2oj
slug: forsaken-mail-docker
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/3GZNPBLImWc/upload/e22e206bea47a471f0ea26dc39fac302.jpeg
tags: 5li05pe26yku566x

---

### **1.简单介绍：**

Forsaken mail 是一个临时邮箱系统，可以创建临时邮箱来收取一些验证码

### 2.域名解析：

这里使用 Cloudflare 解析

添加一条 A 记录，比如 email -&gt; 1.1.1.1

![](https://qiedd.com/wp-content/uploads/2022/05/image-2.png align="left")

随后添加一条 MX 记录 email -&gt; [email.example.com](http://email.example.com)

![](https://qiedd.com/wp-content/uploads/2022/05/image.png align="left")

### 3\. 安装 ：

##### **3.1安装 Docker**

[https://docs.docker.com/engine/install/debian/](https://docs.docker.com/engine/install/debian/)

##### [https://docs.docker.com/engine/install/debian/](https://docs.docker.com/engine/install/debian/)

\# Debian/Ubuntu

curl -fsSL [https://get.docker.com](https://get.docker.com) -o [get-docker.sh](http://get-docker.sh)

\# Arch

pacman -S docker

##### **3.2安装 Caddy**

[https://caddyserver.com/docs/install](https://caddyserver.com/docs/install)

\# Debian/Ubuntu

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https

curl -1sLf '[https://dl.cloudsmith.io/public/caddy/stable/gpg.key](https://dl.cloudsmith.io/public/caddy/stable/gpg.key)' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc

curl -1sLf '[https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt](https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt)' | sudo tee /etc/apt/sources.list.d/caddy-stable.list

sudo apt update

sudo apt install caddy

\# Arch

pacman -S caddy

\# 启动 Docker 服务

systemctl start docker

systemctl enable docker

\# 下载源码

git clone [https://github.com/denghongcai/forsaken-mail](https://github.com/denghongcai/forsaken-mail)

\# 进入目录

cd forsaken-mail

\# 构建镜像

docker build -t forsaken-mail .

\# 运行镜像

docker run -d --name forsaken-mail --restart=always -p 25:25 forsaken-mail

\# 查看容器ip

docker inspect forsaken-mail

\## 找到这里

\## "IPAddress": "172.17.0.3",

\# 修改Caddyfile

vim /etc/caddy/Caddyfile

{

servers :443 {

protocol {

allow\_h2c

experimental\_http3

}

}

servers :80 {

protocol {

allow\_h2c

experimental\_http3

}

}

}

import /etc/caddy/conf.d/\*

\# 创建文件

vim /etc/caddy/conf.d/forsaken-mail

[email.example.com](http://email.example.com) {

reverse\_proxy 172.17.0.3:3000

file\_server

}

\# 启动Caddy

systemctl start caddy

systemctl enable caddy

### 4.搭建完成了