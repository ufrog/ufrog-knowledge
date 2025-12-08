# 设置「GOPROXY」代理

由于众所周知的原因，我们在用「GO」语言的时候，经常会发现需要加载的第三方包无法下载，这个时候我们可能设置一下「GOPROXY」参数。这个参数在「Windows」下和「Linux」下的设置方法是不同的。

首先需要开启「go module」
```shell
go env -w GO111MODULE=on  // Windows
export GO111MODULE=on     // macOS or Linux
```

接着我们就能设置代理了
```shell
go env -w GOPROXY=https://xxxx.xxxx.com,direct    // Windows
export GOPROXY=https://xxxx.xxxx.com              // macOS or Linux
```

下面列几个我们常用的替换地址
```shell
https://goproxy.cn                    // 最常用
https://mirrors.aliyun.com/goproxy/   // 阿里代理
```

总上所述，如果你是在「Windows」下，可以执行命令
```shell
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

而如果是在「macOS」或者「Linux」下，可以执行命令
```shell
export GO111MODULE=on
export GOPROXY=https://goproxy.cn
```

其实大家可以直接上 https://goproxy.cn 也会有使用方法的说明。