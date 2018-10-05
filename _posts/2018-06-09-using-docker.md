---
layout: post
title: "使用Docker"
categories: docker, mysql
---

记录一下[Docker](https://www.docker.com/)常用镜像的使用。

## `MySQL`

``` bash
## 下载镜像
$ docker pull mysql
## 创建容器，设置初始化密码
$ docker run -it -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=xxx --name mysql mysql
## 登陆并创建host可访问的用户
$ docker exec -it mysql mysql -uroot -p 
## MySQL 8之前的版本
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'xxxxxx';
## MySQL 8
## 使用native方式加密，加密方式可通过SELECT Host, User, plugin FROM mysql.user;查看
mysql> ALTER USER 'root'@'%' IDENTIFIED WITH MYSQL_NATIVE_PASSWORD BY 'xxxxxx';
mysql> GRANT ALL ON *.* TO 'root'@'%';
mysql> FLUSH PRIVILEGES;
## host中登陆，需要使用127.0.0.1
$ mysql -uroot -p -h 127.0.0.1
```

## `Gitlab`

``` bash
$ docker pull gitlab/gitlab-ce
$ sudo mkdir /opt/gitlab
$ sudo chown -R xxx:staff /opt/gitlab
$ mkdir config datas logs
$ docker run -it -d -p 80:80 -p 443:443 -p 22:22 --name gitlab -v /opt/gitlab/config:/etc/config -v /opt/gitlab/logs:/var/log/gitlab -v /opt/gitlab/data:/var/opt/gitlab gitlab/gitlab-ce
## 访问 http://localhost
```

## `Zookeeper`

``` bash
$ docker pull zookeeper
$ docker run -it -d -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zk zookeeper
## 连接zookeeper
$ docker exec -it zk zkCli.sh
```

TO BE CONTINUE...
