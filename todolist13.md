
2016年 09月 23日 星期五 09:03:30 CST

1. 隐藏华为软件盘；
2. 正确显示返回和标题栏；
3. 增加返回缩小功能
4. 增加点击聊天缩小功能


2016年 09月 23日 星期五 09:26:38 CST

**有空了解**
[如何用命令行创建 android 项目](http://stackoverflow.com/questions/20801042/how-to-create-android-project-with-gradle-from-command-line)

[adb 查看手机 ip 命令](http://blog.csdn.net/love__coder/article/details/7459811)
`$ adb shell netcfg`

[隐藏虚拟按键](http://blog.sina.com.cn/s/blog_75992b660101kzdj.htm)
status bar : at the top of handset devices
system bar : at the bottom of tablet devices since Android 3.0
navigation bar : since Android 4.0, a devices that provides the navigation bar also has the status bar at the top

[颜色不透明度](http://stackoverflow.com/questions/5445085/understanding-colors-in-android-6-characters)
Hex Opacity Values
    100% — FF
    95% — F2
    90% — E6
    85% — D9
    80% — CC
    75% — BF
    70% — B3
    65% — A6
    60% — 99
    55% — 8C
    50% — 80
    45% — 73
    40% — 66
    35% — 59
    30% — 4D
    25% — 40
    20% — 33
    15% — 26
    10% — 1A
    5% — 0D
    0% — 00

2016年 09月 23日 星期五 14:11:09 CST

[手动旋转屏幕](http://www.jb51.net/article/64735.htm)

建议在res中建立layout-land和layout-port两个文件夹

Q：如何做到手动旋转屏幕，同时又不销毁 Activity，走 onDestroy -> onCreate 的路径？
手动旋转方法：
//横屏设置
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
//竖屏设置
setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);

Q：如何获取当前屏幕方向？
getResource().getConfiguration().orientation

Q：如何实现 TextView 中的内容旋转顺时针旋转 90度？
答：

2016年 09月 23日 星期五 17:12:53 CST

开始按照横屏和竖屏思路进行 直播全屏 和 非全屏功能的改造

1. 在 AndroidManifest.xml 中添加 configuration 和 orientation 属性配置；
2. 重写 onConfigurationChanged 方法；
3. 














