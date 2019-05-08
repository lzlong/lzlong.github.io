---
title: Java小知识点
date: 2019-05-08 10:41:08
tags:
 - java
categories:
 - 笔记
 - java
---

* Collections.addAll() 与 ArrayList.addAll()
    * 大型list添加少量元素时建议使用Collections.addAll()，但当List的size较小时，两种方法没有什么区别，甚至ArrayList.addAll()更好。
    * 添加数组时，没有什么性能差异，添加List时，建议使用ArrayList.addAll()。
