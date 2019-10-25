# _Docker_

## 简介

Docker 是一个开源的应用容器引擎，诞生于 2013 年初，
它基于 Google 公司推出的 Go 语言实现。

Docker 项目的目标是实现轻量级的操作系统虚拟化解决方案。
Docker 的基础是 Linux 容器（LXC）等技术。
Docker 在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。
用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

**镜像** (**_Image_**)

**容器** (**_Container_**)

## 安装

```bash
# https://docs.docker.com/install/linux/docker-ce/ubuntu/
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
apt-add-repository -y -u "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
apt-get -y install docker-ce
```

## 应用

基于 Ubuntu 16.04 创建镜像并部署在线监测系统。

1.  获取镜像

    `sudo docker pull ubuntu:16.04`

1.  列出镜像

    `sudo docker images`

1.  删除镜像

    `sudo docker rmi ubuntu:16.04`

1.  使用镜像来创建一个容器。

    `sudo docker run -it -p 8000:80 ubuntu:16.04 /bin/bash`

    -   `-i, --interactive`

        > Keep STDIN open even if not attached

    -   `-t, --tty`

        > Allocate a pseudo-TTY

    -   `-p, --publish`

        > Publish a container's port(s) to the host

1.  在运行的容器内进行安装配置。

    -   复制文件到容器。

        `sudo docker cp ./setup {CONTAINER_ID}:/root/`

    -   输入 `exit` 命令退出容器。

1.  提交容器副本。

    `sudo docker commit -a="chuaple" -m="message" {CONTAINER_ID} chuaple/ois:v1`

1.  使用新镜像。

    `sudo docker run -it chuaple/ois:v1 /bin/bash`

1.  启动容器。

    `sudo docker run -d -p 8000:80 chuaple/ois:v1`

    -   `-d, --detach`

        > Run container in background and print container id

1.  查看容器。

    `sudo docker ps -a`

1.  导出容器。

    `sudo docker export {CONTAINER_ID} > ois.tar`

1.  导入容器。

    `cat ois.tar | sudo docker import - chuaple/ois:v1`

1.  删除容器。

    `sudo docker rm {CONTAINER_ID}`
