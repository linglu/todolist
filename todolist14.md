
2016年 09月 26日 星期一 09:16:43 CST

[学习 文档化 app 状态数据工具 Pury](https://medium.com/@nikita.kozlov/pury-new-way-to-profile-your-android-application-7e248b5f615e#.3wgyy9h1a)

1. Pury 用于测量多个独立事件之间的时间；
2. 事件可以被注解或者方法调用触发；

2016年 09月 26日 星期一 09:57:04 CST

1. 开完周会议；
2. 发周报；
2. 提交现有代码到 git 服务器； done at 2016年 09月 26日 星期一 11:16:15 CST
3. 将聊天展示功能整合到全屏界面；
4. 添加下拉刷新功能到首页；
5. 完成其他 UI 界面布局；

2016年 09月 26日 星期一 11:16:43 CST

刚才 Simon 演示发现几个 bug，现在先着手解决这个问题


2016年 09月 26日 星期一 14:20:01 CST

着手解决 小米5 和 华为 mate8 的 root 权限的问题

[小米5 root 教程](http://jingyan.baidu.com/article/414eccf66ebfdd6b421f0a4c.html)

华为 mate8 root 教程 尝试使用 root 大师

virtualbox 使用 usb 方法，在 mail.qq.com 的记事本中有

查看软件安装路径：
`>$ dpkg -L 软件名`

[命令行启动虚拟机](http://www.linuxidc.com/Linux/2011-11/48301.htm)
`>$ VBoxManage startvm vm_name`

[关于没有界面的虚拟机的管理方式](http://www.server110.com/virtualbox/201404/9992.html)

手机 root 失败，改日再弄

2016年 09月 26日 星期一 14:56:41 CST

聊天崩溃的情况，不是很好复现，简单判断了一下是否为 null，放到后期再处理
此外，我发现 斗鱼直播 的聊天也只显示了几十条信息的样子

*下面开始做首页下拉刷新的功能*

按：找个时间，将 Toast 的，或者 DebugLog 的输出信息输出到 sd 卡里面

2016年 09月 26日 星期一 18:16:59 CST

首页添加下拉刷新功能；

[关于 SwipeRefreshLayout 的正确使用方式](https://yassironsoftware.com/2014/05/16/how-to-use-swiperefreshlayout-the-right-way/)

windows
http://tech.qq.com/a/20080820/000246.htm
http://www.cnbeta.com/articles/89053.htm
https://www.zhihu.com/question/24960401

2016年 09月 27日 星期二 16:35:09 CST
使用代码实现全屏和退出全屏的方法：此时还会有 titleBar，可以通过设置 Theme 去掉
```
private void full(boolean enable) {
        if (enable) {
            WindowManager.LayoutParams lp =  getWindow().getAttributes();
            lp.flags |= WindowManager.LayoutParams.FLAG_FULLSCREEN;
            getWindow().setAttributes(lp);
            getWindow().addFlags(WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS);
        } else {
            WindowManager.LayoutParams attr = getWindow().getAttributes();
            attr.flags &= (~WindowManager.LayoutParams.FLAG_FULLSCREEN);
            getWindow().setAttributes(attr);
            getWindow().clearFlags(WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS);
        }
    }
```

[android中获得屏幕、视图、任务栏、状态栏的高宽以及屏幕的设置](http://blog.csdn.net/yiyaaixuexi/article/details/6233005)


2016年 09月 27日 星期二 17:14:20 CST
暂时采用下面的方法来进行全屏操作

```
if(Build.VERSION.SDK_INT < 19) { // 19 or above api
  getWindow().getDecorView().setSystemUiVisibility(View.GONE);
} else {
  //for lower api versions.
  View decorView = getWindow().getDecorView();
  int uiOptions = View.SYSTEM_UI_FLAG_HIDE_NAVIGATION | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY;
  decorView.setSystemUiVisibility(uiOptions);
}
```

有空时，测试尽可能多的型号手机，理解官方的[文档](https://developer.android.com/training/system-ui/immersive.html)：

2016年 09月 27日 星期二 19:01:01 CST

今天完成了全屏直播聊天界面的整合以及沉浸式全屏功能

明天开始其他界面 UI 的布局功能实现；










