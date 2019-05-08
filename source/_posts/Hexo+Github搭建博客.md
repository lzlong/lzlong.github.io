---
title: Hexo+Github搭建博客
date: 2019-05-08 10:41:08
categories:
 - github
 - hexo
tags:
 - hexo
 - github
---

### 准备
 * 有一个github账号，没有的话去注册一个；
 * 安装了node.js、npm，并了解相关基础知识；
 * 安装了git for windows（或者其它git客户端）
<!--more-->

### 开始
 * 创建仓库
    * 创建一个名为'你的用户名.github.io'的仓库,将来你的网站访问地址就是 http://你的用户名.github.io 了
    * ps: 仓库名字必须是：username.github.io，其中username是你的用户名
 * 绑定域名(自愿)
 * 配置SSHkey
    * cd 用户地址()/.ssh #检查本机已存在的ssh密钥
    * ssh-keygen -t rsa -C "邮件地址" 生成sshkey
    * .ssh\id_rsa.pub 将文件内容复制到个人设置 -> SSH and GPG keys -> New SSH key
    * ssh -T git@github.com 测试是否成功
        * 如果提示Are you sure you want to continue connecting (yes/no)?，输入yes，然后会看到:
```
Hi liuxianan! You've successfully authenticated, but GitHub does not provide shell access.
```

### Hexo
 * [官网](https://hexo.io/zh-cn/)

#### 安装
 * npm install -g hexo
 * 如果没有npm还需要先安装node

#### 初始化
 * 创建一个hexo文件夹 这个是你的博客代码等的存放文件夹
 * hexo init  在你的文件夹下执行这个命令
 * 执行完成之后会自动下载文件到这个目录
    ```
    hexo g # 生成
    hexo s # 启动服务
    ```
 * 执行以上命令之后，hexo就会在public文件夹生成相关html文件，这些文件将来都是要提交到github去的
 * hexo s # 本地预览服务
 * 执行完成之后 打开http://localhost:4000 即可 如果不能打开可能是端口被占用了, [解决可参考](http://blog.liuxianan.com/windows-port-bind.html)

#### 修改主题
 * [官方主题](https://hexo.io/themes/)
 * 举个例子[hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)
 * 在hexo文件夹下执行
    ```
    git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
    ```
 * 修改_config.yml中的theme: landscape改为theme: yilia，然后重新执行hexo g来重新生成。如果出现一些莫名其妙的问题，可以先执行hexo clean来清理一下public的内容，然后再来重新生成和发布。

#### 上传
 * 配置_config.yml
    ```
    deploy:
      type: git
      repository: git@github.com:liuxianan/liuxianan.github.io.git
      branch: master
    ```
 * 执行 hexo d
 * 如果报 Deployer not found: github 或者 Deployer not found: git 错误则执行npm install hexo-deployer-git --save
 * 如果报
    ```
    warning: LF will be replaced by CRLF in XXXXXXXXXXXXXX.
    ```
    解决
    ```
    git config --global core.autocrlf false
    ```

#### 上传源文件
  * hexo d上传部署到github的其实是hexo编译后的文件，是用来生成网页的，不包含源文件, 也就是只上传了.deploy_git里的文件, 而要上传我们的source, 配置文件, 主题等可以使用分支来完成
  * github新建分支
    ![新建分支](/images/newBranch.png)
    在输入框中填写需要的分支名, 如果没有这个分支会提示创建
  * 设置默认分支
    ![默认分支](/images/默认分支.png)
    在设置里将创建的分支改为默认分支, 这样clone的时候就会默认clone hexo分支下的数据
  * clone之后将.git文件夹之外的文件全部删除, 然后将你本地hexo文件夹下的内容复制过来除了.deploy_git
  * .gitignore 内容如下
  ```
  .DS_Store
  Thumbs.db
  db.json
  *.log
  node_modules/
  public/
  .deploy*/
  ```
  没有创建一个, 有则保证内容一致, 当前文件在hexo根目录下
  * 如果clone过主题文件需要删除主题文件夹下的.git否则不能上传
  * 上传
  ```
  git add .
  git commit –m "add branch"
  git push
  ```

#### 常用命令
 * 常用命令 
     ```
    hexo new "postName" #新建文章
    hexo new page "pageName" #新建页面
    hexo generate #生成静态页面至public目录
    hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
    hexo deploy #部署到GitHub
    hexo help  # 查看帮助
    hexo version  #查看Hexo的版本
    ```

 * 简写
    ```
    hexo n == hexo new
    hexo g == hexo generate
    hexo s == hexo server
    hexo d == hexo deploy
    ```
 * 组合命令
    ```
    hexo s -g #生成并本地预览
    hexo d -g #生成并上传
    ```
### 引用及参考
 * https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html
 * https://blog.csdn.net/sinat_37781304/article/details/82729029
