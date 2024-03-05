---
title: Git 小技巧
date: 
updated: 
tags: git
categories: linux
cover: https://s1.ax1x.com/2023/06/19/pC30gRP.png
---

Git 加速小技巧

访问 GitHub 很慢，我们可以加上代理。

这里以 `V2rayN` 为例，sock5端口号为 10808

给 git 添加上全局代理：

```powershell
.\git.exe config --global http.proxy socks5://127.0.0.1:10808
```

