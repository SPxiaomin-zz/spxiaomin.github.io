---
title: docker入门学习笔记
date: 2017-07-24 15:42:14
categories: ['技术', '后端技术']
tags:
---

## 安装

<https://cr.console.aliyun.com/?spm=5176.1971733.0.2.394b9fbdWjruQ3#/accelerator>

## 镜像

搜索镜像

```shell
$ docker search centos
```

查看本地已有镜像

```shell
$ docker images
```

下载镜像

```shell
$ docker pull centos
```

使用阿里云镜像加速

<https://cr.console.aliyun.com/?spm=5176.1971733.0.2.394b9fbdfuuK1g#/accelerator>

## 容器

创建容器

```shell
$ docker run centos /bin/echo 'hello'
```

创建指定NAME的容器

```shell
$ docker run --name greeting centos /bin/echo 'hello'
```

查看正在运行的容器

```shell
$ docker ps
```

查看所有容器

```shell
$ docker ps -a
or
$ docker ps --all
```

查看最近的容器

```shell
$ docker ps -a -l
or
$ docker ps -a --latest
```

删除容器

```shell
$ docker rm CONTAINER ID
```

查看容器的日志

```shell
$ docker logs NAME
```

持续跟踪容器的日志

```shell
$ docker logs --follow CONTAINER ID
```

停止容器

```shell
$ docker stop NAME
```

重启容器

```shell
$ docker restart NAME
```

开始容器

```shell
$ docker start NAME
```

创建带互动的容器

```shell
$ docker run -i -t centos /bin/bash
or
$ docker run --interactive --tty centos /bin/bash
```

在后台运行的容器

```shell
$ docker run --detach centos ping ninghao.net
```

## 创建镜像

手动创建镜像

```shell
$ docker commit -m '提交的日志' -a '作者名字' CONTAINER ID 用户名/镜像的名字:tag
# tag可以是latest，表示最新的一个版本
```

使用Dockerfile创建镜像

```
FROM centos
MAINTAINER SPxiaomin <3013366498@qq.com>
RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
RUN yum install -y nodejs
```

```shell
$ docker build --tag spxiaomin/nodejs-demo:lastest ./
# 最后面是Dockerfile文件的位置
```

删除主机上的镜像

```shell
$ docker rmi 镜像的名字
e.g. docker rmi spxiaomin/nodejs-demo
```

把镜像推送到Docker hub

```shell
$ docker login
$ docker push spxiaomin/nodejs-demo
```

把镜像推送到阿里云

<https://cr.console.aliyun.com/?spm=5176.1971733.0.2.394b9fbdfuuK1g#/dockerImage/59203/detail>

END.
