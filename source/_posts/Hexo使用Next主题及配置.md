---
title: Hexo使用Next主题及配置
date: 2019-05-08 17:53:48
categories:
 - hexo
tags:
 - hexo
 - next
 - 主题
---
### Hexo配置
 *  配置文件为根目录下_config.yml
 * [配置参数详解](https://hexo.io/zh-cn/docs/configuration), 该地址有配置文件参数的详细介绍再次就不一一列举, 只写我用到的几个
 * 网站
   <table>  <tr><td>参数</td><td>描述</td></tr>  <tr><td>title</td><td>网站标题</td></tr>  <tr><td>subtitle</td><td>网站副标题</td></tr>  <tr><td>description</td><td>网站描述</td></tr>  <tr><td>author</td><td>您的名字</td></tr>  <tr><td>language</td><td>网站使用的语言</td></tr>  <tr><td>timezone</td><td>网站时区。Hexo 默认使用您电脑的时区。时区列表。比如说：America/New_York, Japan, 和 UTC 。</td></tr>  </table>
   其中，description主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。author参数用于主题显示文章的作者。
 * 扩展
    <table>  <tr><td>参数</td><td>描述</td></tr>  <tr><td>theme</td><td>当前主题名称。值为false时禁用主题</td></tr>  <tr><td>deploy</td><td>部署部分的设置</td></tr>  </table>

### Next 主题
 * clone 在hexo根目录下执行
 ```
 git clone https://github.com/iissnan/hexo-theme-next themes/next
 ```
 * 启用 打开根目录配置文件将 theme 改为 next 注意冒号之后的空格 保存之后使用`hexo clean`清除缓存
 * 使用`hexo s --debug`在debug模式下启动服务
   ```
   INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
   ```
   出现上述内容代表启动成功, 使用浏览器访问http://localhost:4000, 查看是否正常运行
   ![成功样式](validation-default-scheme-mac.png)
   出现上述页面证明Next正常加载
 * 语言配置 打开根目录的配置文件将`language `设置成你需要的语言, eg: 简体中文
   ```
   language: zh-Hans
   ```
   配置完成之后主题会在相应的配置文件中解析菜单等的相关词汇, 路径为`themes/next/languages`若配置的语言在这里没有则会默认英文
 * 下文所说主题配置文件为`themes/next/_config.yml`
 * 选择Scheme next提供不同的主题样式, 可以在主题配置文件里选择Scheme的值来展示不同的样式
 * 设置菜单Menu
  1. 内容设置 在主题配置文件里找到 menu 字段, 菜单内容的设置格式是：item name: link。其中 item name 是一个名称，这个名称并不直接显示在页面上，她将用于匹配图标以及翻译。
  ```
  menu:
    home: / || home
    about: /about/ || user
    tags: /tags/ || tags
    categories: /categories/ || th
  ```
    > 若你的站点运行在子目录中，请将链接前缀的 / 去掉

    menu默认菜单为, 保持默认值即可, 需要哪个就将其注释去掉
      * home		#主页
      * archives		#归档页
      * categories		#分类页
      * tags	tags: 	#标签页
      * about	about: 	#关于页面
      * commonweal		#公益 404

  2. 设置菜单显示文本, 上述设置了menu的显示项, 显示文字内容是从next肢体目录下的`languages/{language}.yml`中寻找对应文字显示的, 如果要添加菜单项则要在相关文件下寻找menu字段然后在其下添加, 之后在主题配置文件中添加并显示 eg:
    ```
    menu:
      home: 首页
      archives: 归档
      categories: 分类
      tags: 标签
      about: 关于
      search: 搜索
      commonweal: 公益404
      something: 有料 # 新增项
    ```
  3. menu图标设置
    * 图标对应字段为 menu_icons 格式相同为key: value, key与第一项中的菜单名称对应, value 为Font Awesome图标的名称, enable 控制是否显示图标 key 值大小写要严格匹配
 * 侧栏 sidebar
  1. 位置 sidebar.position
    * left - 靠左放置
    * right - 靠右放置
    > 目前仅 Pisces Scheme 支持 position 配置

  2. 显示时机 sidebar.display
    * post - 默认行为，在文章页面（拥有目录列表）时显示
    * always - 在所有页面中都显示
    * hide - 在所有页面中都隐藏（可以手动展开）
    * remove - 完全移除
    > 已知侧栏在 use motion: false 的情况下不会展示

  * 头像 avatar
    * 网络地址  完整的url
    * 站内地址  将头像放置主题目录下的 source/uploads/ （新建 uploads 目录若不存在）
      配置为：avatar: /uploads/avatar.png, 或者source/images/ 目录下
      配置为：avatar: /images/avatar.png
 * 菜单页面 添加菜单页面
  * 标签页面
    * 新建页面 `hexo new page tags` 会在 source 文件夹下生成 tags 的文件夹以及 index.md 文件
    * 设置页面类型, 在文件头部添加 type 值
    ```
    ---
    title: 标签
    date: 2014-12-22 12:39:04
    type: "tags"
    ---
    ```
    * 修改菜单, 在主题配置文件中将 menu 菜单添加 tags 项, 用于展示在侧边栏
  * 其他页面, 需要添加其他页面时和 tags 页面操作相同
  * 404 页面, 按照上文添加 404 页面, 然后添加以下内容
  ```html
  <!DOCTYPE HTML>
  <html>
  <head>
    <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="robots" content="all" />
    <meta name="robots" content="index,follow"/>
    <link rel="stylesheet" type="text/css" href="https://qzone.qq.com/gy/404/style/404style.css">
  </head>
  <body>
    <script type="text/plain" src="http://www.qq.com/404/search_children.js"
            charset="utf-8" homePageUrl="/"
            homePageName="回到我的主页">
    </script>
    <script src="https://qzone.qq.com/gy/404/data.js" charset="utf-8"></script>
    <script src="https://qzone.qq.com/gy/404/page.js" charset="utf-8"></script>
  </body>
  </html>
  ```
  部署到 github 之后当输入一个找不到的地址时就会自动出现 404 页面, 内容时腾讯的寻找丢失儿童的公益 404 页面
 * 动画效果 motion
  ```
  motion:
    enable: true # 开启动画效果
    enable: false # 关闭动画效果
  ```
 * 背景动画
   ```
   # canvas_nest
   canvas_nest: true //开启动画
   canvas_nest: false //关闭动画
   # three_waves
   three_waves: true //开启动画
   three_waves: false //关闭动画
   ```
