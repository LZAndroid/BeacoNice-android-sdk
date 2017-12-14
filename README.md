</br>
</br>
</br>
</br>
<p align="center">
  <img src="https://github.com/LZAndroid/BeacoNice-android-sdk/blob/master/image/beaconice.png">
</p>
</br>
</br>
</br>
</br>


# BeacoNice-android-sdk

# Android SDK 集成指南

## Step 1 SDK下载  

## Step 2 导入SDK  

将 jar 包复制到工程的 libs 目录下面，  

![导入](https://github.com/LZAndroid/BeacoNice-android-sdk/blob/master/image/screenshort.png)  
由于 jar 包依赖Volley、Gosn，请在build.gradle文件中添加以下依赖：

    dependencies {
        compile fileTree(dir: 'libs', include: ['*.jar'])
        compile 'com.mcxiaoke.volley:library:1.0.19'
        compile 'com.google.code.gson:gson:2.6.2'
    }

## Step 3 添加用户权限配置    

需要用户允许打开蓝牙与网络的相关权限，在工程 AndroidManifest.xml 文件中添加如下权限

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

## Step 4 使用  

    //初始化BleManager对象，并打开蓝牙
    BleManager.init(MainActivity.this);
    //获取对象
    BleManager bleManager = BleManager.getInstance();
    //开始扫描
    bleManager.scanLeDevice(true);
    //设置扫描回调监听,返回附近Beacon绑定的相关数据
    bleManager.setBeaconsInfoCallback(new BleManager.OnBeaconsInfoCallback() {
        @Override
        public void onScanCallback(ArrayList<BeaconInfo> mBeaconArrayInfo) {

            for(BeaconInfo b : mBeaconArrayInfo){
                Log.d(TAG, b.getCoverage());                    //Beacon的覆盖范围   
                Log.d(TAG, b.getDistance());                    //Beacon与手机的实时距离
                Log.d(TAG, b.getMajor());                       //Beacon Major
                Log.d(TAG, b.getMinor());                       //Beacon Minor
                AudioInfo audioInfo = b.getAudioInfo("zh");     //Beacon绑定的音频数据
                ...
                ...
            }
        }
    });


### 官网：<http://www.beaconice.cn/>