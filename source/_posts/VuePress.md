---
title: 快速上手 VuePress
date: 
updated:
tags: vue
categories: 前端
cover: https://vuepress.vuejs.org/hero.png
---



# 快速上手 VuePress

## 依赖环境

- pnpm 7.29.3
- vue  3.3.4
- vuepress 2.0.0-beta.62

## 安装：

- <b>步骤1: </b> 创建并进入一个目录

- <b>步骤2:</b> 初始化项目

  ```sh
  pnpm init
  ```

- <b>步骤3:</b> 添加本地依赖

  ```sh
  pnpm add -D vuepress@next @vuepress/client@next vue
  ```

- <b>步骤4:</b> 在 `package.json` 文件中添加 script

  ```json
  {
    "scripts": {
      "docs:dev": "vuepress dev docs",
      "docs:build": "vuepress build docs"
    }
  }
  ```

- <b>步骤5:</b> 创建第一篇文档

  新建一个 docs 目录

  ```sh
  mkdir docs
  ```

  新建一个 markdown 文件，并写入内容

  ![](../FILES/VuePress.md/image-20230823133339149.png)

- <b>步骤6:</b> 在本地启动服务器

  ```sh
  pnpm docs:dev
  ```

{% note success %}
VuePress 会在 `http://localhost:8080/` 启动一个热重载的开发服务器。当你修改你的 Markdown 文件时，浏览器中的内容也会自动更新。
{% endnote %}

整个 VuePress 搭建完成！