# 设置「npm」国内镜像加速
又再一次由于众所周知的原因，在使用 `npm` 下载包的时候往往并不理想，所以我们也需要把包的下载源替换成国内的镜像站以提高下载速度并且保证成功率。

## 1. 直接替换注册地址
我们可以执行命令直接替换源
```shell
npm config set registry http://mirrors.cloud.tencent.com/npm/           // 腾讯镜像源
npm config set registry https://registry.npmmirror.com                  // 淘宝镜像源
npm config set registry https://mirrors.huaweicloud.com/repository/npm/ // 华为云镜像源
```
以上三个只要选择其中一个就可以了，执行后可以执行命令验证
```shell
npm config get registry
```
只要输出的是你设置的镜像源地址即设置成功，可以开始愉快的 `install` 了。

## 2. 安装「cnpm」工具
第二种方法是直接安装由阿里定制的 `cnpm` 工具，可以执行以下命令
```shell
npm install -g cnpm --registry=https://registry.npmmirror.com
```
之后使用以下命令安装包
```shell
cnpm install xxx
```
其实这和设置了淘宝的镜像源效果是一样的，所以还是比较推荐修改设置镜像源的方式提高下载包的速度。