---
title: nodejs 更新
date: 
updated: 
tags: nodejs
categories: 前端
cover: https://s1.ax1x.com/2023/06/20/pC83wcj.png
---

# nodejs 更新

1. 查看版本

```sh
node -v
```

![image-20230530140912644](../FILES/nodejs更新.md/image-20230530140912644.png)

2. 清除npm缓存

```sh
npm cache verify
```

![image-20230530141003682](../FILES/nodejs更新.md/image-20230530141003682.png)

3. 安装 nvm 

> 专门用来管理版本

下载地址：[Releases · coreybutler/nvm-windows (github.com)](https://github.com/coreybutler/nvm-windows/releases)

![image-20230530142308794](../FILES/nodejs更新.md/image-20230530142308794.png)

下载 nvm-setup.zip 文件，接着直接下一步...

安装成功后，输入命令

```sh
nvm --version
```

![image-20230530142403267](../FILES/nodejs更新.md/image-20230530142403267.png)

4. 安装新版 nodejs

```sh
nvm install lts
```

![image-20230530142835262](../FILES/nodejs更新.md/image-20230530142835262.png)

5. 切换nodejs

```sh
nvm use 18.16.0
```

