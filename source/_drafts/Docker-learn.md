---
title: Docker 学习
tags: [docker]
categories: [docker]
date: 2021-03-01 17:46:19
---


> 记录 Docker 的基本用法

<!-- more -->

## 1.参考
* 1.[Install Docker Desktop on Mac](https://docs.docker.com/docker-for-mac/install/)
* 2.[Docker 入门教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)
* 3.[Get started](https://docs.docker.com/get-started/02_our_app/)


## 2.基本步骤
### 1.Build the app’s container image
* 1.下载源码
* 2.新增 `Dockerfile`
* 3.执行 `docker build` 命令

### 2.Start an app container

#### 1.用已有的 image 去创建新的 container
* 1.执行 `docker run -dp  <本地端口>:<docker 端口> --name <container name> <image name>/<tag name>` 命令, 如: `docker run -dp 8080:8080 --name jenkins-test jenkins/jenkins:lts-alpine`


### 3.Container CLI Command
* 1.Get all containers information: `docker ps -a`
* 2.Start a container: `docker start <container-id>`
* 3.Stop the container: `docker stop <container-id>`
* 4.Remove container: `docker rm <container-id>`

### 4.[SSH into a Container](https://phase2.github.io/devtools/common-tasks/ssh-into-a-container/)
```
There is a docker exec command that can be used to connect to a container that is already running.

Use docker ps to get the name of the existing container
Use the command `docker exec -it <container name> /bin/bash` to get a bash shell in the container
Generically, use `docker exec -it <container name> <command>` to execute whatever command you specify in the container.
```

## 3.Build Angular app in a docker container
* 1.[Build and run Angular application in a Docker container](https://wkrzywiec.medium.com/build-and-run-angular-application-in-a-docker-container-b65dbbc50be8)


## 4.包管理

> 由于 Docker 默认会阻止不安全连接方式（http）, 所以 MacOS 要在 `~/.docker/daemon.json` 文件中加入 `"insecure-registries": [ "address:port" ],`

### 1.参考
* 1.[Using Nexus 3 as Your Repository – Part 3: Docker Images](https://blog.sonatype.com/using-nexus-3-as-your-repository-part-3-docker-images)

### 1.用 `Nexus` 做包管理器
* 1.`docker login -u admin -p admin123 your-repo:port`

* 2.Pull and Push

```
docker tag hello-world:latest your-repo:port/hello-world:latest

docker push your-repo:port/hello-world
 
docker pull your-repo:port/hello-world
```


## 5.文件传输
### 1.参考
* 1.[How to copy files to/from a container](https://kb.sitecore.net/articles/383441)

### 2.To copy a file from the local file system to a container

```
docker cp <src-path> <container>:<dest-path> 
```

### 3.To copy a file from the container to the local file system

```
docker cp <container>:<src-path> <local-dest-path> 
```

