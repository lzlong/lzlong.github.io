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
