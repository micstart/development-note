1. 基础知识
1.1什么是Java内存泄漏？  
    Java的一个重要优点就是通过垃圾收集器(Garbage Collection，GC)自动管理内存的回收，程序员不需要通过调用函数来释放内存。当不再使用的对象无法被GC回收时即存在内存泄漏。
1.2Java对象引用强度  
    强引用(Strong Reference):
        代码之中普遍存在的，类似：“Object objectRef = new Obejct”，这种引用，只要强引用还存在，永远不会被GC清理。
    软引用(SoftReference):
        用来描述一些还有用，但并非必须存在的对象，当JVM内存不足时（内存溢出之前）会被回收，如果执行GC后，还是没有足够的空间，才会抛出内存溢出异常。
        User user = new User();  
        SoftReference<Object> softReference  = new SoftReference<Object>(user);  
        softReference.get();
    弱引用(WeakReference):
        用来描述一些还有用，但并非必须存在的对象，它的强度会被软引用弱些，被弱引用关联的对象，只能生存到下一次GC前，当GC工作时，无论内存是否足够，都会回收掉弱引用关联的对象。
    虚引用(PhantomReference):
        虚引用称为“幻影引用”，它是最弱的一种引用关系，一个对象是否有虚引用的存在，完全不会对生存时间构成影响，虚引用的get方法总是返回null。为一个对象设置虚引用关联的唯一目的就是希望能在这个对象被GC回收时收到一个系统通知。
参考资料：  
    http://www.importnew.com/22264.html
    https://www.ibm.com/developerworks/cn/java/l-JavaMemoryLeak/

2. Android常见内存泄漏  
2.1静态变量
    把Android组件实例赋值给静态变量，当这个静态变量在组件生命周期结束后没有清空，就导致内存泄漏。
    例如：将Activity赋值给静态变量，导致Activity无法释放。
2.2单例
    单例对象中引用了具有生命周期的对象，导致其不能释放。
2.3非静态内部类
    非静态内部类持有外部类的引用，当外部类生命周期结束后内部类未被释放时会导致内存泄漏。
    例如：
        1.在Activity中创建的非静态的内部类XXHandler，其发送的消息均持有Activty的引用。
        2.在Activity中创建的非静态的内部类XXThread，其实例持有Activty的引用。
2.4资源未关闭
    IO流、Cursor、Bitmap、Dialog、属性动画
参考资料：
    http://allenwu.itscoder.com/oom-and-solution

3. MAT工具使用
3.1获取heap文件
    在Eclipse或Android Studio工具的Devices中，选中目标进程点击"Dump HPROF file"按钮导出hprof文件。
    也可以通过adb命令生成hprof文件：
        adb shell am dumpheap com.demo.memoryleak /data/local/tmp/com.demo.memoryleak.hprof
        adb pull /data/local/tmp/com.demo.memoryleak.hprof
        hprof-conv com.demo.memoryleak.hprof com.demo.memoryleak_new.hprof
    需要将 HPROF 文件从Android 格式转换为Java SE HPROF 格式:
        hprof-conv android.hprof java.hprof

3.2分析heap文件
~~~
    OQL语句：
        SELECT * FROM [ INSTANCEOF ]	<class_name> [ WHERE <filter-expression>]
    例如：
        select * from android.view.View
        select * from instanceof android.view.View
        select * from instanceof android.app.Activity
        select * from instanceof android.app.Fragment
        select * from instanceof android.graphics.Bitmap
        select * from instanceof java.lang.Thread
        select * from instanceof com.qiku.android.contacts.cache.CustomAsyncTask
        // select * from instanceof java.io.Closeable
        select * from instanceof java.io.InputStream
        select * from instanceof java.io.OutputStream
        select * from instanceof java.io.Reader
        select * from instanceof java.io.Writer
        select * from instanceof android.database.CursorWrapper
        select * from instanceof android.database.AbstractCursor
~~~
参考资料：  
    http://help.eclipse.org/neon/index.jsp?topic=/org.eclipse.mat.ui.help/welcome.html
    https://mingjunli.gitbooks.io/mat/content/%E8%A1%A5%E5%85%85/SELECT.html
    http://www.lightskystreet.com/2015/09/01/mat_usage/
    http://androidperformance.com/2015/04/11/AndroidMemory-Usage-Of-MAT.html
    http://androidperformance.com/tags/MAT/
    http://dev.qq.com/topic/57d14047603a5bf1242ad01b
    https://zhuanlan.zhihu.com/p/25213586

查看内存命令：
~~~
adb shell "dumpsys meminfo com.demo.memoryleak"
adb shell "procrank | grep com.demo.memoryleak"
~~~
USS	Unique Set Size         进程独占的内存
PSS	Proportional Set Size   PSS= USS+ 按比例包含共享库
RSS	Resident Set Size       SS= USS+ 包含共享库
VSS	Virtual Set Size        VSS= RSS+ 未分配实际物理内存  
参考资料：
http://gityuan.com/2016/01/02/memory-analysis-command/

