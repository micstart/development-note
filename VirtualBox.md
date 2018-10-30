主板BIOS设置中开启VT支持（需CPU支持）
https://program-think.blogspot.com/2014/09/system-vm-6.html

1安装增强功能（Guest Additions）

2性能优化
2.1设置-系统-处理器中，处理器数量设为2
2.2设置-系统-硬件加速中，半虚拟化接口设为“KVM”
2.3设置-显示-屏幕中，显存设为128M，勾选“启用3D加速”
2.4设置-储存-控制器:SATA中，勾选“使用主机输入输出缓存”
https://blog.csdn.net/shangpusp/article/details/46762491
https://www.jianshu.com/p/77435e67980c

3无法识别USB设备问题
3.1运行regedit，删除HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Class\{36FC9E60-C465-11CF-8056-444553540000}中的UpperFilters
3.2删除C:\Windows\System32\drivers\usbfilter.sys
3.3右键安装C:\Program Files\Oracle\VirtualBox\drivers\USB\filter\VBoxUSBMon.inf
https://www.bbsmax.com/A/ZOJPGkRozv/
https://bytefreaks.net/windows/virtualbox-failed-to-attach-the-usb-device-to-the-virtual-machine
