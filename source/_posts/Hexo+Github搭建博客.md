---
title: Hexo+Github搭建博客
date: 2019-05-08 10:41:08
categories:
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
  package-lock.json
  ```
  没有创建一个, 有则保证内容一致, 当前文件在hexo根目录下
  * 如果clone过主题文件需要删除主题文件夹下的.git否则不能上传
  * 上传
  ```
  git add .
  git commit –m "add branch"
  git push
  ```

#### 更换机器
 * clone 源文件
 * npm install -g hexo 全局安装 hexo
 * npm i 安装 依赖包

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

#### 写作
 * md语法
   语法不在此详细介绍可以参考下面的地址
   [MD语法入门](https://www.jianshu.com/p/399e5a3c7cc5)
    [Markdown基本语法](https://www.jianshu.com/p/191d1e21f7ed)
    [官网教程](http://www.markdown.cn/)
 * hexo特性
  * Front-matter
    hexo 创建的md文件会在最上方默认有一个用 `---` 分隔的区域这个区域就是 Front-matter
    默认有三个参数
    ```
    title: 标题
    date: 2019-05-08 10:41:08
    tags:
    ```
    这个区域预定义的参数有  (不清楚原因不支持md的表格语法, 所以 换成了`<table>`标签)
    <table>    <tr><td>参数</td><td>描述</td></tr>    <tr><td>layout</td><td>布局</td></tr>    <tr><td>title</td><td>标题</td></tr>    <tr><td>date</td><td>建立日期</td></tr>    <tr><td>updated</td><td>更新日期</td></tr>    <tr><td>comments</td><td>开启文章的评论功能</td></tr>    <tr><td>tags</td><td>标签(不适用于分页)</td></tr>    <tr><td>categories</td><td>分类(不适用于分页)</td></tr>  <tr><td>permalink</td><td>覆盖文章网址</td></tr>    </table>
    如果需要修改或新增默认参数可以在scaffolds文件夹下的post.md中修改(hexo new "" 创建默认使用post模板)
    其中，分类和标签需要区别一下，分类具有顺序性和层次性，也就是说 Foo, Bar 不等于 Bar, Foo；而标签没有顺序和层次.
    ```
    categories:
    - Diary
    tags:
    - PS3
    - Games
    ```
  * layout
  `hexo new ""` 默认使用`post`布局, 生成的文件在`/source/_post`中
  hexo 有三种默认布局: `post`, `page`, `draft`生成的文件路径不同, 自定义布局的路径和post路径相同
  <table>  <tr> <td>布局</td> <td>路径</td> </tr> <tr><td>`post`</td> <td>`source/_posts`</td> </tr> <tr><td>`page`</td> <td>`source`</td></tr>  <tr><td>`draft`</td> <td>`source/_drafts`</td></tr>  </table>
  所以new命令应该是`hexo new [layout] <title>` 默认layout是post

   * page
   `hexo new page "newPage"`用于另起一页, 会在source下创建一个名为newPage的文件夹和index.md的文件, newPage的路径就是`http://xxx.xxx/board`
   * draft
   `hexo new draft newpage`draft文件是草稿文件, 并不会直接展示在首页列表, 要预览草稿文件需要`hexo server --draft`, 发表草稿文件则为`hexo publish draft newpage`

 * 图片
  * 少量图片可以在source文件夹下新建images文件夹然后将图片复制到文件夹下, 引用方式为`![title](images/a.jpeg)`
  * 大量图片时需要在根目录的_config文件中将`post_asset_folder`置为true, 这样在`hexo new ""`时会随之生成一个同名文件夹, 可以将图片复制到文件夹下, 引用方式`![](a.jpeg)`这种方式并不会将图片展示在首页列表中.
  需要在首页列表中展示图片则引用方式如下:
  ```
  {% asset_img a.jpeg This is an example image %}
  ```
  当在主题中设置首页列表不显示文章全部信息时大概率上面的方式也不会在首页列表中显示图片
  搭建暂时就只有这些内容, 我会在另一篇文章中详细介绍我的hexo和主题是如何配置的

### 引用及参考
 * https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html
 * https://blog.csdn.net/sinat_37781304/article/details/82729029
