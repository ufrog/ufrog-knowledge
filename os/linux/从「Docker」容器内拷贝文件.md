# 从「Docker」容器内拷贝文件
我们在启动部署镜像的时候经常需要修改镜像内的配置文件，但是这个配置文件从哪里来呢？必须直接从镜像中拷贝出来进行修改，然后再作为文件卷定义进去是完美的。我们这次就以部署「Nginx」作为样例进行操作。

## 1. 部署临时容器
拷贝文件必须是从容器中拷贝，不能直接从镜像中拷贝，所以我们这里需要先部署一个临时的容器。
```shell
docker run --name tmp-nginx -d nginx
```
查看一下容器是不是正常起来了，如果正常起来了就继续下一步

## 2. 拷贝文件
如果容易已经跑起来了，我们就可以从里面拷贝文件了
```shell
docker cp tmp-nginx:/etc/nginx/nginx.conf ./nginx.conf
//docker cp ${docker-conatiner}:${container-path} ${host-path}
```
以上的命令就是拷贝容器文件到宿主机目录

## 3. 删除临时容器
最后临时的容器总是要删除的，这个就是「docker」的优势，删除之后什么都不剩下，非常适合我这个强迫症
```shell
docker stop tmp-nginx
docker rm tmp-nginx
```
这样就完成了，非常的简单