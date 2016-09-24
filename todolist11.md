
2016年 09月 20日 星期二 09:28:46 CST

预研 RecyclerView 的自动滑动到底部功能和与输入法的结合功能；

第一步：实现滑动

done at 2016年 09月 20日 星期二 10:10:58 CST 

第二步：[控制滑动速度](http://blog.csdn.net/a86261566/article/details/50906456)

因为 
RecyclerView 的 smoothScrollToPosition 方法实际调用的是 LayoutManager 中的 smoothScrollToPosition 方法

所以
可以通过复写 LayoutManager 中的 smoothScrollToPosition 方法来实现控制滑动速度的目的

done at 2016年 09月 20日 星期二 10:30:24 CST

第三步：实现输入法键盘打开时，RecyclerView 也跟着顶上去

Q：如何让 EditText 自动获取焦点 或者 取消获取焦点
答：通过在 xml 文件中 EditText 控件下面添加 <requestFocus /> 语句可以让 EditText 获取焦点
通过在 EditText 控件的父布局中添加如下语句可以实现取消自动获取焦点
```
android:focusable="true"
android:focusableInTouchMode="true"
```

Q：如何控制 EditText 获取焦点后自动弹出输入法或者不弹出输入法
答：EditText 获取焦点后会自动弹出输入法，不获取焦点则不弹出输入法；

第三步目前还未找到实现方法，但是已经实现了每一条消息发出去之后，新消息能显示在最底部的效果

2016年 09月 20日 星期二 11:31:25 CST

整合完毕，pitaya 中可以实现发出的消息自动滚动到底部，并且可以控制其速度。
此外还实现了本人发出的消息 sender 红色显示

下午继续实现视频全屏显示和发送框的调整

2016年 09月 20日 星期二 11:54:34 CST

完成发送框的点击和颜色布局

2016年 09月 20日 星期二 15:04:51 CST

打算使用新的 Activity 来实现全屏功能，
开始研究 Activity 之间的跳转动画以及传参问题；

思路：使用同一个 Activity

2016年 09月 20日 星期二 16:08:54 

1. 点击全屏后，将视频播放的 LayoutParam 设置为全屏，并全屏显示播放，隐藏其他图标
2. 给全屏过程添加动画效果；
3. 在全屏下的操作，使用新的 Helper 代理操作；

[修改 View 的 LayoutParams 的操作](http://blog.csdn.net/u013675234/article/details/50465634)

首先 view.getLayoutParams();
然后修改 width 和 height 后，
最后将修改后的 Params 设置回 view 中
view.setLayoutParams();

[设置全屏的三种方式](http://www.2cto.com/kf/201109/104363.html)

在 super() 和 setContentView 之前

``` 
requestWindowFeature(Window.FEATURE_NO_TITLE);//隐藏标题栏
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,WindowManager.LayoutParams.FLAG_FULLSCREEN);//
隐藏状态栏
```

2016年 09月 20日 星期二 17:23:32 CST

开始整合全屏功能到 Pitaya 中

2016年 09月 20日 星期二 17:48:52 CST
















