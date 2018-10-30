1. 主板BIOS设置中开启VT支持（需CPU支持）  
https://program-think.blogspot.com/2014/09/system-vm-6.html

2. 安装增强功能（Guest Additions）

3. 性能优化  
  3.1 设置-系统-处理器中，处理器数量设为2  
  3.2 设置-系统-硬件加速中，半虚拟化接口设为`KVM`  
  3.3 设置-显示-屏幕中，显存设为128M，勾选`启用3D加速`  
  3.4 设置-储存-控制器:SATA中，勾选`使用主机输入输出缓存`  
https://blog.csdn.net/shangpusp/article/details/46762491  
https://www.jianshu.com/p/77435e67980c

4. 无法识别USB设备问题  
4.1 运行regedit，删除  
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Class\{36FC9E60-C465-11CF-8056-444553540000}`中的`UpperFilters`  
4.2 删除`C:\Windows\System32\drivers\usbfilter.sys`  
4.3 右键安装`C:\Program Files\Oracle\VirtualBox\drivers\USB\filter\VBoxUSBMon.inf`  
https://www.bbsmax.com/A/ZOJPGkRozv/  
https://bytefreaks.net/windows/virtualbox-failed-to-attach-the-usb-device-to-the-virtual-machine  
