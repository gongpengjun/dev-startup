# Mac上安装MySQL

## 0. 安装方式概览

- 通过MySQL官方源码安装
- 通过MySQL官方二进制安装
- 通过brew安装
- 通过docker安装

## 1. 通过docker安装

### 安装docker

在Docker官网下载 [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop) 安装包来完成docker的安装

完成安装后，就获得了 Docker  Docker Engine, Docker CLI client, Docker Compose等

查看docker和docker-compose命令行工具

```
$ docker --version
Docker version 20.10.0, build 7287ab3
$ docker-compose --version
docker-compose version 1.27.4, build 40524192
```

## 2. 通过docker-compose管理MySQL

### 2.1 编写docker-compose.yml文件

选在一个根目录，假设选择当前用户目录`~`，下文都假设根目录为`~`

在根目录下编写文件docker-compose.yml，内容如下：

```
---
version: '2.1'
services:
  mysql:
    image: mysql:5.6.33
    container_name: local-mysql
    hostname: mysql
    restart: always
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: "yes"
      MYSQL_DATABASE: test
    volumes:
      - "./local_mysql/storage:/var/lib/mysql"
      - "./local_mysql/etc/mysql:/etc/mysql"
    ports:
      - "3306:3306"
```

> 可通过命令 `$ cat ~/docker-compose.yml` 检查其输出是否如上所示

> 也可下载 [docker-compose.yml](mysql_on_mac/docker-compose.yml) 直接使用

### 2.2 使用docker-compose启动mysql

```
$ cd ~
$ docker-compose up -d
Creating local-mysql ... done
```

MySQL就启动成功了，下次开机重启也自动启动

## 3. 验证：连接MySQL

使用MySQL图形化客户端 [Sequel Pro.app](https://www.sequelpro.com/) 登录的参数如下：

```
Host: 127.0.0.1
Username: root
Password: (空白，无密码)
Database: test
Port: 3306
```
