---
title: Android AppLink调研分析 
date: 2017-02-07
categories: Android 
tags: Android
---

## 1. AppLinks介绍
---
谷歌2015年的google大会上宣布了一个新特性：允许开发者将app和他们的web域名关联。这一举措是为了最小化用户遇到“打开方式”对话框的概率。

### AppLinks优点：
用户点击普通的web链接能够直接调起指定通过验证的app，大大提高调起率

### AppLinks缺点：
1. 只支持原生的Android M以上的机器上（非原生的基本不支持）
2. App Links开发者必须维护一个与app相关联的网站
3. App Links的开关在系统设置中可以关闭

## 2. AppLinks具体实现
### AppLinks实现原理
***
![yuanlitu](/_attatchassets/Applink_img/yuanlitu.jpg)

	*安装或者升级package过程:
	1. PackageManager对即将安装的apk做常规的验证。
	2. 如果成功，这个package将被安装，同时发出一个带有android.intent.action.INTENT_FILTER_NEEDS_VERIFICATION的广播intent，intent中还携带有该package的信息。
	3. Intent Filter Verifier的广播接收器将获取这个广播。
	4. 从package的标签中编译出一个特有主机名的列表。
	5. verifier尝试从每个特有的主机名中获取assentlinks.json。
	6. 每一个被获取的JSON文件都会检查它的application ID和安装包的证书。
	7. 只有当所有文件同时满足时，才会发送成功信息到PackageManager，否则失败。
	8. PackageManager存储结果。

### 前提准备条件
***
	* 自己的域名同时开通ssl通道（https环境）
	* 有上传到域名指向服务器的权限 

### 实现方法
***
#### 客户端实现
1. 设置Activity的Intent Filter, 设置android:autoVerify="true"

```
 <activity android:name="com.baidu.baidumaps.DeepLinkActivity">
      <intent-filter android:autoVerify="true">
           <action android:name="android.intent.action.VIEW" />
           <category android:name="android.intent.category.DEFAULT" />
           <category android:name="android.intent.category.BROWSABLE" />
           <data android:scheme="http" android:host="client.map.baidu.com" />
           <data android:scheme="https" android:host="client.map.baidu.com" />
      </intent-filter>
 </activity>
```
	
#### 服务端实现
服务端端要上传assetlinks.json文件到.well-known/文件下
[assetlinks文件内容](http://client.map.baidu.com/.well-known/assetlinks.json)
	
	[
		{
			"relation": [
			"delegate_permission/common.handle_all_urls"
			],
			"target": {
			"namespace": "android_app",
			"package_name": "com.baidu.BaiduMap",
			"sha256_cert_fingerprints": [
				"A6:EF:81:7B:FD:6C:08:34:42:A1:49:85:6E:51:03:6F:69:12:C2:DB:6B:60:09:DB81:27:CD:D6:41:E2:95:A9"
				]
			}	
		}
	]

其中sha256_cert_fingerprints获取命令
> keytool -list -v -keystore BaiduMap/keystore/bdmobile.keystore

## 3. 测试方法
1. 验证Digital AssetLinks files的有效性可以通过谷歌的api
```
https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=https://client.map.baidu.com&relation=delegate_permission/common.handle_all_urls
```
![assetlink](/_attatchassets/Applink_img/assetlinks.jpg)
2. 使用web URI intent看能否调起
```
adb shell am start -a android.intent.action.VIEW \
    -c android.intent.category.BROWSABLE \
    -d "http://client.map.baidu.com"
```
3. 检查是否和系统建立连接
```
adb shell dumpsys package d
```

## 4. 参考文献
1. [Handling App Links](https://developer.android.com/training/app-links/index.html)
2. [Android M App Links:implementation,drawbacks and solutions](http://blog.hokolinks.com/android-m-app-links-implementation-drawbacks/)
3. [platform_frameworks_base/packages/StatementService/src/com/android/statementservice/](https://github.com/android/platform_frameworks_base/tree/master/packages/StatementService/src/com/android/statementservice)


