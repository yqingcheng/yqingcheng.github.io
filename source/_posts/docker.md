---
title: docker
date: 
updated:
tags: linux
categories: linux
cover: ./images/docker.png
---
# docker

首先卸载掉旧版本

```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```

## 下载

参考文章：http://www.taodudu.cc/news/show-5875688.html?action=onClick

### 添加仓库

文件: `/etc/apt/sources.list`

通过 vim 打开文件，并在最后添加源

```sh
sudo vim /etc/apt/sources.list
```

![Img](../FILES/docker.md/img-20230617154152.png)

### 安装

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

![Img](../FILES/docker.md/img-20230617154328.png)

等待安装完毕...(耗时46秒)

### 启动 docker

```sh
systemctl start docker
```

会提示输入密码，deepin 也可以人脸识别。

### 查看 docker 版本

```sh
docker --version
```

![Img](../FILES/docker.md/img-20230617154722.png)

docker-ce 查看

```sh
docker version
```


![Img](../FILES/docker.md/img-20230617161038.png)

### 切换国内加速器

这里采取阿里云加速地址: https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors

{%note success no-icon flat%} 

details 配置文件说明

{% endnote %}

1. 当你下载安装的Docker Version不低于1.10时，建议直接通过daemon config进行配置。
2. 使用配置文件 <span style="background-color: yellow">/etc/docker/daemon.json</span>（没有时新建该文件）
    ```json
    {
        "registry-mirrors": ["<your accelerate address>"]
    }
    ```
3. 重启 Docker Daemon

{%note info no-icon flat%} 

具体操作如下：

{% endnote %}

需要管理员权限：sudo 

```sh
sudo vim /etc/docker/daemon.json
```

![Img](../FILES/docker.md/img-20230617161249.png)

重新启动 docker

```sh
sudo systemctl daemon-reload
```

```sh
sudo systemctl restart docker
```







