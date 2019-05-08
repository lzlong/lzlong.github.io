---
title: Chocolatey的安装与使用
date: 2019-05-08 10:41:08
tags:
---
### 前言
 * windows 下的apt-get
 * [官网](https://chocolatey.org/)
### 安装
 在线安装
 * 管理员打开cmd输入命令
    ```
      powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
 使用官网命令安装失败, 然后使用上边的命令安装成功, 也可以使用官网的PowerShell命令试一下,离线安装没有读懂
 * 自定义安装位置
   以上都是安装到了默认位置C:\ProgramData\Chocolatey，如果现在其他地方安装Chocolatey的话，需要新建一个环境变量ChocolateyInstall，值是你希望安装到的文件夹。然后手动创建这个文件夹。然后再运行上面的命令。如果已经安装了，可以再次运行安装命令，这样可以重新安装到你指定的位置。
 * 升级Chocolatey
 ```
    choco upgrade chocolatey
 ```
### 使用
 * 安装命令
 ```
    choco install ruby
    cinst ruby
 ```
 * 搜索
 ```
    clist ssh
    choco list ssh
 ```
 * 卸载
 ```
    choco uninstall ssh
    cuninst ssh
 ```
