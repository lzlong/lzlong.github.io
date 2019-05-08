---
title: 百度地图api使用
date: 2019-05-08 10:41:08
tags:
---
### 配置
 * sdk包 按需下载
 * 权限
     ``` java
     //获取设备网络状态，禁用后无法获取网络状态
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    //网络权限，当禁用后，无法进行检索等相关业务
    <uses-permission android:name="android.permission.INTERNET" />
    //读取设备硬件信息，统计数据
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    //读取系统信息，包含系统版本等信息，用作统计
    <uses-permission android:name="com.android.launcher.permission.READ_SETTINGS" />
    //获取设备的网络状态，鉴权所需网络代理
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    //允许sd卡写权限，需写入地图数据，禁用后无法显示地图
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    //这个权限用于进行网络定位
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
    //这个权限用于访问GPS定位
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    //获取统计数据
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    //使用步行AR导航，配置Camera权限
    <uses-permission android:name="android.permission.CAMERA" />
    //程序在手机屏幕关闭后后台进程仍然运行
    <uses-permission android:name="android.permission.WAKE_LOCK" />
     ```
 * 配置文件
    ```
    <!-- 秘钥 -->
    <application>  
        <meta-data  
            android:name="com.baidu.lbsapi.API_KEY"  
            android:value="开发者 key" />  
    </application>
    <!-- 定位服务 -->
    <service
        android:name="com.baidu.location.f"
        android:enabled="true"
        android:process=":remote"/>
    ```
 * 使用
    ``` java
    //在使用SDK各组件之前初始化context信息，传入ApplicationContext   
    SDKInitializer.initialize(this);
    //自4.3.0起，百度地图SDK所有接口均支持百度坐标和国测局坐标，用此方法设置您使用的坐标类型.
    //包括BD09LL和GCJ02两种坐标，默认是BD09LL坐标。
    SDKInitializer.setCoordType(CoordType.BD09LL);
    ```
 其余的就是根据情况使用了.
