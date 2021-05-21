---
title: Docker笔记
date: 2021-05-14 10:24:39
categories:
 - Docker
tags:
 - Docker
---
## Docker 核心
 * Image： 和 windows 的那种 iso 镜像相比，Docker 中的镜像是分层的，可复用的，而非简单的一堆文件迭在一起（类似于一个压缩包的源码和一个 git 仓库的区别）。

 * Container： 容器的存在离不开镜像的支持，他是镜像运行时的一个载体（类似于实例和类的关系）。依托 Docker 的虚拟化技术，给容器创建了独立的端口、进程、文件等“空间”，Container 就是一个与宿机隔离 “容器”。容器可宿主机之间可以进行 port、volumes、network 等的通信。

 * Repository： Docker 的仓库和 git 的仓库比较相似，拥有仓库名、tag。在本地构建完镜像之后，即可通过仓库进行镜像的分发。常用的 Docker hub 有 https://hub.docker.com/ 、 https://cr.console.aliyun.com/ 等。

### 修改docker安装地址 (未测试)
 * 用管理员身份打开cmd窗口，然后运行命令：
 ```mklink /j "C:\Program Files\Docker" "D:\docker-image"```
  在此之前要先创建"D:\docker-image"目录，最后安装docker就可以了。
### 更改镜像安装目录
 * 停止docker 图标右键 Quit Docker Desktop
 * wsl --list -v 查看
 * 导出数据 ```wsl --export docker-desktop-data "F:\Docker\wsl\data\docker-desktop-data.tar"```
 * 删除旧数据(数据未备份前请谨慎操作) ```wsl --unregister docker-desktop-data```
 * 导入数据到新盘 ```wsl --import docker-desktop-data "F:\Docker\wsl\data" "F:\Docker\wsl\data\docker-desktop-data.tar" --version 2``` 命令执行完毕后会在当前目录下会生成一个 ext4.vhdx 虚拟磁盘.