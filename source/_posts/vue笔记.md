---
title: '''vue笔记'''
date: 2021-08-18 11:05:40
categories:
tags:
---
* 事件修饰符
  ```
    .stop 阻止冒泡（通俗讲就是阻止事件向上级DOM元素传递）
    .prevent 阻止默认事件的发生
    .capture 捕获冒泡，即有冒泡发生时，有该修饰符的dom元素会先执行，如果有多个，从外到内依次执行，然后再按自然顺序执行触发的事件。
    .self 将事件绑定到自身，只有自身才能触发，通常用于避免冒泡事件的影响
    .once 设置事件只能触发一次，比如按钮的点击等。
    .passive 该修饰符大概意思用于对DOM的默认事件进行性能优化，根据官网的例子比如超出最大范围的滚动条滚动的。
    .native 在父组件中给子组件绑定一个原生的事件，就将子组件变成了普通的HTML标签，不加'.native'事件是无法触发的。
  ```
* 按键修饰符
  ```
    .enter => // enter键
    .tab => // tab键
    .delete (捕获“删除”和“退格”按键) => // 删除键
    .esc => // 取消键
    .space => // 空格键
    .up => // 上
    .down => // 下
    .left => // 左
    .right => // 右
  ```
* ${}
  使用 ${} 拼接字符串 字符串整体 不使用 ''/"" 包裹 使用 `` 包裹
### element-ui 相关
* element 主动收起时间及日期选择器
 ```
    if(t.$refs.datePicker){
      t.$refs.datePicker.hidePicker();
    }
 ```
### vant-ui 相关

### 其它依赖 相关
#### vue-pdf
 * 请求url需要加 hander  pdf.createLoadingTask({ url: url, httpHeaders:this.headers, CMapReaderFactory });
#### pdfh5 
 * 请求url需要加 hander
 ```
 this.pdfh5 = new Pdfh5("#pdfPage", {
        pdfurl: url,
        goto: 0,
        type:"fetch", //需要写 不写 加不上 header
        httpHeaders: this.headers
      });
 ```
 * pdf 的div 需要 高度样式 不然只展示一页