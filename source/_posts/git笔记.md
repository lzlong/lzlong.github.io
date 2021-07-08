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
    原因是路径中存在 / 的符号转义问题，false就是不转换符号,默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题

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
 * 创建本地分支
   * git branch 分支名
   例如：git branch dev，这条命令是基于当前分支创建的本地分支，假设当前分支是master(远程分支)，则是基于master分支创建的本地分支dev。

 * 删除本地分支(必须保证不在删除的分支上，才能进行删除)
   ``` git branch -d dev ```

 * 切换到本地分支
   ``` git checkout 分支名 ```
   例如：git checkout dev，这条命令表示从当前master分支切换到dev分支。

 * 创建本地分支并切换
   ``` git checkout -b 分支名 ```
   例如：git checkout -b dev，这条命令把创建本地分支和切换到该分支的功能结合起来了，即基于当前分支master创建本地分支dev并切换到该分支下。

 * 提交本地分支到远程仓库
 ``` git push origin 本地分支名 ```
   例如： git push origin dev ，这条命令表示把本地dev分支提交到远程仓库，即创建了远程分支dev。

 * 删除远程分支
   ``` git push --delete origin dev ```
 * 撤销 commit
  ``` 
    git reset --soft HEAD~1 
    HEAD~1 表示上一个版本，即上一次的commit
    如果进行两次的commit，想要都撤回，可以使用HEAD~2
    --soft
    不删除工作空间的改动代码 ，撤销commit，不撤销git add file
    --hard
    删除工作空间的改动代码，撤销commit且撤销add

    另外一点，如果commit注释写错了，先要改一下注释，有其他方法也能实现，如：

    git commit --amend
    这时候会进入vim编辑器，修改完成你要的注释后保存即可。
  ```
 * 查看所有分支
  git branch -a
 * clone 远程分支
  git checkout -b dev origin/dev