# 清除「Docker」缓存
用了一段时间「Docker」之后，那些过期的镜像会一直残留在系统中，久而久之会占用大量的磁盘空间。这个时候我们就需要来清理一下「Docker」的缓存。

一般我们会在目录`/var/lib/docker/overlay2`看到这些镜像文件，但是随便删文件肯定是不行的，好在「Docker」提供了清除缓存的命令：

```
[root@localhost /]# docker system prune -a
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated to them
  - all build cache

Are you sure you want to continue? [y/N]
```
这里选`Y`就可以清空缓存了。其实上面已经写清除了会删除哪些内容：
1. 所有已经停止的容器
2. 所有没有被使用的网络配置
3. 所有没有关联到容器的镜像
4. 所有创建时的缓存

以下再罗列一些查看磁盘信息的命令，以备查询所用
```
df -hl  #查看磁盘剩余空间
df -h   #查看每个根路径的分区大小
du -sh [目录名]    #返回该目录的大小
du -sm [目录名]    #返回该目录文件夹总数
du -h --max-depth=1 [目录名]  #查看该目录下所有文件大小
```