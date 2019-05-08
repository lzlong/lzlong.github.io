---
title: git笔记
date: 2019-05-08 10:59:05
categories:
 - github
 - git
tags:
 - git
 - github
---

记录git使用过程中遇到的问题和解决办法

<!--more-->

 * git add 时会报一个错误
    ```
    warning: LF will be replaced by CRLF in XXXXXXXXXXXXXX.
    ```
    解决
    ```
    git config core.autocrlf false
    ```
    原因是路径中存在 / 的符号转义问题，false就是不转换符号默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题

 * 解决github每次push都需要登录的问题
  * github需要添加SSHkey
  * 原因是在建立远程仓库或者克隆项目时，使用的是HTTPS方式 ，HTTPS方式push不会保存用户名和密码
  1. git remote -v  查看远程连接的方式
  2. git remote rm origin 删除原先HTTPS的连接方式
  3. GitHub仓库复制SSH的地址  Clone or download -> Use SSH -> 复制地址
  4. git remote add origin SSH地址
  5. git push 提交代码, 如果提示
  ```
  fatal: The current branch hexo has no upstream branch.
  To push the current branch and set the remote as upstream, use

     git push --set-upstream origin hexo
  ```
  需要执行 git push --set-upstream origin hexo 把本地分支关联到远程分支
