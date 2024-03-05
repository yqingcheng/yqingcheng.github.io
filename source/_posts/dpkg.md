---
title: dpkg
date: 
updated:
tags: [linux, 包管理器]
categories: linux
cover: https://s1.ax1x.com/2023/06/20/pC8Zzk9.png
---



# 卸载

删除软件包，并保留.postrm和.list文件.

```sh
sudo dpkg -r ${名称}
```

清除所有文件，包括.postrm和.list文件.

```sh
sudo dpkg -P ${名称}
```

查看是否卸载完毕

```sh
sudo dpkg -l ${名称}
```

