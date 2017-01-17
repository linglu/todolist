
2016年 11月 04日 星期五 15:08:37 CST

HPROF Viewer 界面

1. Shallow Size 指的是该对象本身占用内存的大小 
2. Retained Size 代表该对象被释放后，垃圾回收器能回收的内存总和 

2016年 11月 07日 星期一 16:14:51 CST

<GC_Reason>   <Amount_freed>, <Heap_stats>,         <External_memory_stats>,   <Pause_time>
GC_CONCURRENT freed 2049K,    65% free 3571K/9991K, external 4703K/5261K,      paused 2ms+2ms


<GC_Reason> <GC_Name>             <Objects_freed>(<Size_freed>) AllocSpace Objects, <Large_objects_freed>(<Large_object_size_freed>) <Heap_stats> LOS objects, <Pause_time(s)>
Explicit    concurrent mark sweep GC freed 104710(7MB) AllocSpace objects,          21(416KB) LOS objects,                           33% free, 25MB/38MB,      paused 1.230ms total 67.216ms


2016年 11月 07日 星期一 17:45:28 CST


[Memory Monitor](https://developer.android.com/studio/profile/am-memory.html)

作用：
  显示内存分配图
  显示 GC 事件
  初始化 GC 事件
  快速测试与过度 GC 相关的 app 变慢
  快速测试 app 崩溃是否与内存溢出有关

Noun：
	Garbage collection roots
	dominator tress
	
<= Android 4.3 Dalvik Vm
Android 4.4, ART VM is option, Dalvik VM is default
\>= Android 5.0 ART VM

Dalvik VM : mark-and-sweep scheme
ART VM : generational scheme + mark-and-sweep scheme


2016年 11月 08日 星期二 10:32:02 CST

1. this$0 表示内部类的意思
2. target 表示线程的意思

* 查找内存泄漏的步骤：

	1. 触发一次 GC；
	2. 导出 hprof 文件；
	3. 查看 hprof 文件，看是否存在我们我们期望已经回收的 Activity；

* 内存泄漏的几种类型：

	1. 静态变量引起的内存泄漏；
	2. 非静态内部类引起的内存泄漏；
	3. 资源未关闭引起的内存泄漏；

* 引用类型

  强引用：永远不会回收
  软引用：内存不足时才回收
  弱引用：GC 一次将被回收
  虚引用：先加入引用队列再回收

* *.hprof 的查看方法
  左上角找到期望会被回收的类(Class Name)；
  右上角找到类的实例对象(Instance)；
  下面 Reference Tree 可以找到该实例对象的被引用路径














