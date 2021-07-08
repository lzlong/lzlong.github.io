---
title: Android笔记
date: 2021-05-26 13:59:44
categories:
  Android
tags:
  Android
---
### 7.0级以上 URI 访问改变
 * 7.0 调用安装应用时出现 FileUriExposedException ，文件Uri暴露异常 需要使用 FileProvider,  原安装代码为
  ```java
  private void installAPK() {
      String fileName = xxxx;
      String directory = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DOWNLOADS).getPath();
      File apkFile = new File(directory+fileName);
      if (!apkFile.exists()){
          Toast.makeText(MyApplication.getContext(),"安装包文件不存在",Toast.LENGTH_SHORT).show();
          return;
      }
      Intent intent = new Intent(Intent.ACTION_VIEW);
      //安装完成后，启动app
      intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
      intent.setDataAndType(Uri.fromFile(apkFile), "application/vnd.android.package-archive");
      startActivity(intent);
  }
  ```
 * 解决
  1. 在 AndroidManifest.xml 文件的 application 中添加
  ```xml
  <provider
      android:name="androidx.core.content.FileProvider"
      android:authorities="包名.fileprovider" <!-- 内容为标识 String 代码中会 将其作为参数 -->
      android:exported="false"
      android:grantUriPermissions="true">
      <meta-data
          android:name="android.support.FILE_PROVIDER_PATHS"
          android:resource="@xml/provider_paths" />
  </provider>
  ```
  2. 在 res 的 xml 包中创建 provider_paths.xml 文件
  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <paths xmlns:android="http://schemas.android.com/apk/res/android">
      <external-path name="sdcard_root" path="."/>
  </paths>
  ```
  其中paths下的子节点含义：

    |  子节点 |  含义  |
    |  ----  | ----  |
    |<root-path>|设备的根目录 new File("/")|
    |<files-path>|Context.getFileDir()|
    |<catch-path>|Context.getCatchDir()|
    |<external-path>|Environment.getExternalStorageDirectory()|
    |<external-files-path>|Context.getExternalFilesDirs()|
    |<external-catch-path>|Context.getExternalCatchDirs()|
  3. 安装代码改为
  ```java
    private void installAPK() {
        String fileName = xxx;
        String directory = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DOWNLOADS).getPath();
        File apkFile = new File(directory+fileName);
        if (!apkFile.exists()){
            Toast.makeText(MyApplication.getContext(),"安装包文件不存在",Toast.LENGTH_SHORT).show();
            return;
        }
        Intent intent = new Intent(Intent.ACTION_VIEW);
        //安装完成后，启动app
        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
            intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
            Uri uri = FileProvider.getUriForFile(this, this.getPackageName() + ".fileprovider", apkFile);//第二个参数要和Mainfest中<provider>内的android:authorities 保持一致
            intent.setDataAndType(uri, "application/vnd.android.package-archive");
        } else {
            intent.setDataAndType(Uri.fromFile(apkFile), "application/vnd.android.package-archive");
        }
        startActivity(intent);
    }
  ```
  4. AndroidManifest.xml 文件中添加必要的权限：
  ```xml
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES"/>
  ```