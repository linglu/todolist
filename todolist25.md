
2016年 10月 27日 星期四 11:52:17 CST

Q: 为什么在 Demo 中可以使用硬件加速，而在自己的 Demo 中却不能
答：发现了问题，在 demo 的 activity_play.xml 文件中，
com.tencent.rtmp.ui.TXCloudVideoView 控件中有一个属性
```
android:visibility="gone"
```
这个属性加上去之后，无论是否硬件加速都能正常显示。但是如果不加，
那么只有在硬件加速为 false 时才能正常显示；
此外，除了这个属性，com.tencent.rtmp.ui.TXCloudVideoView 控件
的 background 属性，也应该是透明的，不能有其他颜色，否则显示不出来；

Q: 

2016年 10月 27日 星期四 14:09:34 CST

重新自制一份 Live 用于直播项目，去除不关紧要的细节，例如哪个对象先初始化等等

列出可能影响 相同代码的 app 导致不同行为的变量因素：

1. Android 手机版本
2. App 版本


不同 app 的比较维度：

1. minSdkVersion，最低支持的 android 版本
2. 

待续

2016年 10月 27日 星期四 18:20:48 CST

刚刚发布了新版本，使用新的 直播SDK

下面开始弄 windows 下的 code review 操作过程 

1. 安装最近的 PHP 稳定版本，下载地址：http://windows.php.net/download/
2. 配置 php 环境变量；
已在其他地方完成 

2016年 10月 28日 星期五 09:28:52 CST

1. 重构 LiveBroadcastActivity.java

使用若干个 Helper 
* EnterRoomHelper.java - 进入房间、退出房间
* IMHelper.java - 发送聊天信息、接收聊天信息、聊天人数等

2016年 10月 28日 星期五 10:07:41 CST

1. 先开始解决几个 bug 问题

* Fragment 点击穿透的题，两个地方； done 
* 直播返回的点击问题；done
* 全屏标题栏的区域问题； 待定
* 全屏的抽屉按钮问题； done 

2016年 10月 28日 星期五 13:51:10 CST

[关于 android 中的线程的创建与销毁](http://blog.csdn.net/lienyin/article/details/50157471)

1. 如果在一个 Activity 中使用了 Handler，那么退出时需要移除掉
   handler.post(Runnable Thread);
   handler.removecallbacks(Runnable Thread);
   
2. Timer的销毁

a）调用timer的cancle方法。你可以从程序的任何地方调用此方法，甚至在一个
timer task的run方法里；
b）让timer线程成为一个daemon线程（可以在创建timer时使用new Timer(true)
达到这个目地），这样当程序只有daemon线程的时候，它就会自动终止运行；
c）当timer相关的所有task执行完毕以后，删除所有此timer对象的引用（置成
null），这样timer线程也会终止；
d）调用System.exit方法，使整个程序（所有线程）终止。

Q：如何销毁 Timer 和 Handler 产生的线程？


2016年 10月 28日 星期五 14:59:42 CST

开发个老师版本的 apk，主要用于观看聊天功能；

如何用 ./gradlew 不同版本的 apk



















