---
title: pnpm 安装与使用
date: 
updated:
tags: 包管理器
categories: 前端
cover: https://s1.ax1x.com/2023/06/20/pC8GJfS.png
---

# pnpm 

## pnpm install 和 pnpm add

pnpm add 和 pnpm install 命令的本质是相同的，都可以用来安装依赖包。它们的区别在于用法和语法。

pnpm add 命令会将要安装的依赖包加入到 package.json 文件的 dependencies 或者 devDependencies 中，并且可以指定包的版本。例如：

```cmd
pnpm add react@16.8.0
```

pnpm install 命令通常用来安装项目中已有的 package.json 文件中的依赖包。如果没有指定包的版本，则会安装最新版本的依赖包。例如：

```cmd
pnpm install
```

这个命令会安装 package.json 文件中的所有依赖包。

总的来说，pnpm add 命令更加灵活，可以实现指定版本安装，同时更新 package.json 文件。pnpm install 命令更加简洁，适用于快速安装已有的依赖包。

## pnpm 换源与更新

以下出现报错信息：

> ERR_PNPM_REGISTRIES_MISMATCH  This modules directory was created using the following registries configuration: {"default":"https://registry.npm.taobao.org/"}. The current configuration is {"default":"https://mirrors.cloud.tencent.com/npm/"}. To recreate the modules directory using the new settings, run "pnpm install".

删除项目中的 node_module 文件夹

重新使用命令生成

```cmd
pnpm install 
```

然后再次尝试

```cmd
pnpm add ${依赖名}
```

