---
title: node配置
date: 2022-03-12 19:48:25
categories:
tags:
---
### node配置
* 安装
* 配置 安装目录下 新建 node_global 和 node_cache 文件夹
* 设置全局目录和缓存目录，创建完两个空文件夹之后，打开cmd命令窗口，输入
 ···
    npm config set prefix "~\nodejs\node_global"

    npm config set cache "~\nodejs\node_cache"
 ···
 配置结果 在 \.npmrc  文件中 修改配置 修改文件
* 环境变量 
  新建 NODE_PATH 内容为 ~\nodejs\node_modules 路径
  修改【用户变量】下【Path】中的 npm 修改为【~\nodejs\node_global】
* 安装淘宝的cnpm镜像
···npm install -g cnpm --registry=https://registry.npm.taobao.org···
* 安装切换镜像的工具：nrm
···npm install nrm -g···
然后通过nrm ls命令查看npm的仓库列表,带*的就是当前选中的镜像仓库：
···
  npm ---------- https://registry.npmjs.org/
  yarn --------- https://registry.yarnpkg.com/
  tencent ------ https://mirrors.cloud.tencent.com/npm/
  cnpm --------- https://r.cnpmjs.org/
  taobao ------- https://registry.npmmirror.com/
  npmMirror ---- https://skimdb.npmjs.com/registry/
···
通过nrm use taobao来指定要使用的镜像源
通过nrm test npm来测试速度