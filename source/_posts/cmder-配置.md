---
title: cmder 配置
date: 2022-03-12 19:49:14
categories:
tags:
---
### cmder 配置
* 添加环境变量
在环境变量path中添加cmder的路径
* 添加cmder到右键菜单
以管理员模式打开cmd，并且进入到Cmder.exe所在的目录，执行如下命令添加到右键菜单
```Cmder.exe /REGISTER ALL```
* 修改命令输入提示符'λ'为'$'
修改~\cmder\config\cmder_prompt_config.lua 文件，将 'λ' 修改为 'λ'
```  ```
* 解决中文乱码
按 win + alt + p 键或点击默认右下角 settings 选项打开设置界面

找到 Startup 选项下的 Environment，追加这些命令
```
set PATH=%ConEmuBaseDir%\Scripts;%PATH%
set LANG=zh_CN.UTF-8
set LC_ALL=zh_CN.utf8
chcp utf-8
```
* 添加自定义的命令
将Linux中常用的la ll等命令添加到cmder中。
修改D:\cmder\config\user-aliases.cmd文件，添加如下语句：
```
l=ls --show-control-chars
la=ls -aF --show-control-chars
ll=ls -alF --show-control-chars
ls=ls --show-control-chars -F
```
* 快捷键
    ```
    利用Tab，自动路径补全；
    利用Ctrl+T建立新页签；利用Ctrl+W关闭页签;
    利用Ctrl+Tab切换页签;
    Alt+F4：关闭所有页签
    Alt+Shift+1：开启cmd.exe
    Alt+Shift+2：开启powershell.exe
    Alt+Shift+3：开启powershell.exe (系统管理员权限)
    Ctrl+1：快速切换到第1个页签
    Ctrl+n：快速切换到第n个页签( n值无上限)
    Alt + enter： 切换到全屏状态；
    Ctr+r 历史命令搜索
    ```
* settings
 1. startup -> specified named task {cmder::Cmder}
 2. General -> Fonts 去掉Monospace选项
 3. Features -> Transparency Active window transparency