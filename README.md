# BeacoNice-android-sdk

#Android SDK 集成指南

##Step 1 SDK下载  
<http://www.beaconice.cn/>


##Step 2 导入SDK  

将 jar 包复制到工程的 libs 目录下面，  
![导入](Capture.PNG)  
由于 jar 包依赖Volley、Gosn，请在build.gradle文件中添加以下依赖：

    dependencies {
        compile fileTree(dir: 'libs', include: ['*.jar'])
        compile 'com.mcxiaoke.volley:library:1.0.19'
        compile 'com.google.code.gson:gson:2.6.2'
    }

##Step 3 添加用户权限配置    

需要用户允许打开蓝牙与网络的相关权限，在工程 AndroidManifest.xml 文件中添加如下权限

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

##Step 4 使用  

    //初始化Blescan对象，并打开蓝牙
    BleScan.init(MainActivity.this);
    //获取对象
    bleScan = BleScan.getInstance();
    //开始扫描
    bleScan.scanLeDevice(true);
    //设置扫描回调监听
    bleScan.setOnBeaconsInfoListener(new BleScan.OnBeaconsInfoListener() {
        @Override
        public void onBeaconsInfoChange(ArrayList<BeaconInfo> mBeaconArrayInfo) {
            beaconArrayInfo.clear();
            for(BeaconInfo b : mBeaconArrayInfo){
                Log.d(TAG, b.getCoverage());
                Log.d(TAG, b.getDistance());
                Log.d(TAG, b.getMajor());
                Log.d(TAG, b.getMinor());
            }
        }
    });