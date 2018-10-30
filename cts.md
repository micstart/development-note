# Android环境搭建
https://source.android.com/setup/build/initializing

1. 安装Java
```
sudo apt-get update
sudo apt-get install openjdk-8-jdk
```
2. 安装android sdk  
2.1 下载SDK工具包  
2.2 查看所有可用包  
`./sdkmanager --list --proxy=http --proxy_host=xx.xx.xx.xx --proxy_port=xxx`  
2.2 使用命令行下载需要的库  
```
./sdkmanager --install "platform-tools" --proxy=http --proxy_host=xx.xx.xx.xx --proxy_port=xxx
./sdkmanager --install "build-tools;28.0.2" --proxy=http --proxy_host=xx.xx.xx.xx --proxy_port=xxx
./sdkmanager --install "platforms;android-27" --proxy=http --proxy_host=xx.xx.xx.xx --proxy_port=xxx
```
3. 设置环境变量  
```
sudo gedit /etc/profile
export ANDROID_SDK_ROOT=/home/wangyao/env/android_sdk
export PATH=$PATH:$ANDROID_SDK_ROOT/build-tools/28.0.2
export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools
export PATH=$PATH:$ANDROID_SDK_ROOT/tools/bin
source /etc/profile
```
4. 其它  
4.1 adb devcies no permissions (verify udev rules)  
运行：  
`sudo gedit /etc/udev/rules.d/51-android.rules`  
写入以下内容并保存：  
`SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", MODE="0666"`  
运行：  
`sudo chmod a+r /etc/udev/rules.d/51-android.rules`  
参考：  
https://developer.android.com/studio/run/device

# CTS测试
1. 下载并解压CTS包  
https://source.android.com/compatibility/cts/setup  
https://source.android.com/compatibility/cts/run

2. 执行CTS测试：  
`./cts-tradefed`  
运行某个模块：  
`run cts -m CtsDevicePolicyManagerTestCases`  
运行单条用例：  
`run cts -m CtsDevicePolicyManagerTestCases -t com.android.cts.devicepolicy.ManagedProfileTest#testManagedContactsPolicies --skip-preconditions`  

