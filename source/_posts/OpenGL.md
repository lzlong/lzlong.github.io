---
title: OpenGl
date: 2019-05-08 10:41:08
tags:
---
### GLSurfaceView
#### 特性
 1. 提供并且管理一个独立的Surface。
 2. 提供并且管理一个EGL display，它能让opengl把内容渲染到上述的Surface上。
 3. 支持用户自定义渲染器(Render)，通过setRenderer设置一个自定义的Renderer。
 4. 让渲染器在独立的GLThread线程里运作，和UI线程分离。
 5. 支持按需渲染(on-demand)和连续渲染(continuous)两种模式。
 6. GPU加速：GLSurfaceView的效率是SurfaceView的30倍以上，SurfaceView使用画布进行绘制，GLSurfaceView利用GPU加速提高了绘制效率。
 7. View的绘制onDraw(Canvas canvas)使用Skia渲染引擎渲染，而GLSurfaceView的渲染器Renderer的onDrawFrame(GL10 gl)使用opengl绘制引擎进行渲染。

#### 使用
 * 可直接使用GLSurfaceView, 如果有复杂操作也可继承重载
 * onCreate时设置Renderer, 使用setRenderer()方法
 * 设置RenderingMode
    * RENDERMODE_CONTINUOUSLY, 刷新的帧率是60FPS，16ms就重绘一次
    * RENDERMODE_WHEN_DIRTY,被动渲染，在surfaceCreate的时候会绘制一次，之后只有在调用requestRender或者onResume等方法主动请求重绘时才会进行渲染

### GLRender
