# 安装「Docker-CE」.md
装完Docker一顿折腾之后，发现Docker版本已经很旧了，现在Docker已经改成「Docker-CE」和「Docker-EE」顾名思义，CE是开源免费版本，而EE是企业版。那么我们来把原来的Docker更新一下吧。

## 1. 删除原有版本
要安装新的Docker-CE，首先必须要删除原来安装的Docker
```
[root@localhost /]# yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
```
可以多跑几下，跑到说找不到这些包就可以了

## 2. 预处理
首先更新一下yum，以及为了添加新的软件源，安装一下包
```
[root@localhost /]# yum update
[root@localhost /]# yum install -y yum-utils device-mapper-persistent-data lvm2
```
然后添加Docker的软件源
```
[root@localhost /]# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

## 3. 安装
这里就很简单了
```
[root@localhost /]# yum install docker-ce
```
网上说需要一起装`docker-ce-cli`和`containerd.io`，但是经过实践，这些是依赖包，会自动安装

## 4. 加入用户组
需要将用户加入`docker`的用户组，才能正常使用Docker
```
[root@localhost /]# usermod -aG docker ${USER_NAME}
```
将`${USER_NAME}`替换成你自己的用户即可，笔者这里是需要gitlab-runner做发布，所以将`gitlab-runner`用户加入了`docker`用户组

## 5. 启动服务
到这里已经很简单了
```
[root@localhost /]# systemctl enable docker
[root@localhost /]# systemctl start docker
```
实现开机启动，并启动服务，可以验证安装是否成功
```
[root@localhost /]# docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

[root@localhost /]#
```
证明已经成功了

## 6. 安装compose
这一步是可选项，我们一般会用docker-compose来进行镜像的制作，执行命令
```
[root@localhost /]# curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
先别急着复制命令，我们这里看到命令里面有个`1.26.2`，这是笔者当时最新的版本，这个版本可以按需修改，也可以到[官网](https://github.com/docker/compose)去查看最新的版本，安装完之后赋权
```
[root@localhost /]# chmod +x /usr/local/bin/docker-compose
```
全部完成之后可以查看安装结果
```
[root@localhost /]# docker-compose version
docker-compose version 1.26.2, build eefe0d31
docker-py version: 4.2.2
CPython version: 3.7.7
OpenSSL version: OpenSSL 1.1.0l  10 Sep 2019
[root@localhost /]#
```
如果安装完成之后，命令无法使用，可以手动做一个关联
```
[root@localhost /]# ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
到这里安装就已经全部完成了