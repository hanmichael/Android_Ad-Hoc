#基于Google的开源项目wifi_tether分离出来的adhoc发起组网独立模块
##master分支说明
目前可以使用，发起的adhoc网络SSID为：AndroidTether，无密码。
此项目还有很多需要优化的地方，我还得慢慢研究，先达到可以使用的要求，然后再看如何进行修改。
###使用要求
手机需要有ROOT权限，并且给本软件授权，点击发起组网即可，关闭的话点击关闭组网即可。

##develop分支使用说明
发起的adhoc网络同master

###使用步骤
####导入adhoclibrary库到自己的项目当中
修改自己app的gradle文件中的applicationId为"com.googlecode.android.wifi.tether"
在src/main文件夹中建立名为jniLibs的文件夹，然后再在jniLibs文件夹中建立armeabi文件夹，在armeabi文件夹中放入libwtnativetask.so库
简要说明路径为：app/src/main/jniLibs/armeabi/libwtnativetask.so

####在自己项目的AndroidManifest.xml文件中做如下配置：
1.加入权限：
```xml
    <uses-permission android:name="android.permission.WRITE_INTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.CHANGE_WIMAX_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIMAX_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
```
2.配置：
```xml
<application
          android:name="com.googlecode.android.wifi.tether.TetherApplication"
          ...
          />
```
3.加入：
```xml
<service
         android:enabled="true"
         android:name="com.googlecode.android.wifi.tether.TetherService" />
<receiver
       android:name="com.googlecode.android.wifi.tether.TetherServiceReceiver"
       android:exported="false">
         <intent-filter>
             <action android:name="com.googlecode.android.wifi.tether.intent.MANAGE" />
         </intent-filter>
    </receiver>
```
####使用
发起adhoc组网：
```java
AdhocControl.start(getApplicationContext());
```
关闭adhoc组网：
```java
AdhocControl.stop(getApplicationContext());
```
