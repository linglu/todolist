

2016年 08月 31日 星期三 09:17:51 CST

1. [添加 Logger 控件用于日志记录](https://github.com/orhanobut/logger)
 
学习 Logger 控件的使用

Q：wtf 是什么意思？Logger.wtf("")
答：wtf(https://developer.android.com/reference/android/util/Log.html) 的意
思是：what a terrible failure.

Q：Logger.log(DEBUG, "tag", "message", throwable)？答：DEBUG 指定提示级
别，tag 拼接在已有 tag 后面，message 显示在消息区第一行，throwable 指出
错误信息以及回调栈，具体可参见
[wiki](http://192.168.1.19/w/android/technical/lib/logger/)

Q：Logger 对于 list、map、set 的输出格式
答：
对 list 的输出格式：*[first_ele, second_ele, thrid_ele]*
对 map 的输出格式：*{1=first_ele, 2=second_ele, 3=thrid_ele}*
对 set 的输出格式：*[second_ele, first_ele, thrid_ele]*
具体可参见[wiki](http://192.168.1.19/w/android/technical/lib/logger/)

Q：Logger.t("").d("")
答：具体可参见[wiki](http://192.168.1.19/w/android/technical/lib/logger/)
t 后的参数，如果是字符串，则拼接至 已有 tag 后面
如果是数字，则表示 methodCount

Q：Logger.e(exception, "message")
答：类似于 Logger.log() 参数为 "message" throwable 的情况

Q：methodCount 是什么意思？
答：methodCount 是显示 Logger 方法链的数量，如果 methodOffset 不为 0, 则显示偏移后的

Q：methodOffset 是什么意思？
答：methodOffset 表示从调用该 Logger 语句的方法开始开始，忽略调用栈上面的几个方法不显示

Q：Timber 是什么意思？

=== 

2016年 09月 01日 星期四 09:25:11 CST

后续有空学习(https://www.zhihu.com/question/26239412)
===

今天开始进入实际项目开发阶段

[RecyclerView 的相关学习](blog.csdn.net/lmj623565791/article/details/45059587)

[support_v7 代码 demo](home/linky/IDE/sdk/extras/support/samples/Support7Demo)

Q：LayoutManger 中 getSpanCount 的含义？
答：getSpanCount 表示获取布局中的列数；

使用 CardView 解决名片样式布局问
https://developer.android.com/training/material/lists-cards.html#Dependencies


2016年 09月 01日 星期四 14:16:54 CST

Q：RecyclerView 如何实现横向滑动，并且添加 divider？
答：在LinearLayoutManger 中 setOrientation(HORIZONTAL)，
   然后再在 Devider 中做相应处理

Q：onDrawOver 是什么意思？与 onDraw 有什么区别？
答：onDrawOver 绘制在最上层，所以它的绘制位置并不受显示，
[具体可见](http://blog.piasy.com/2016/03/26/Insight-Android-RecyclerView-ItemDecoration/)

Q：ItemDecoration 子类的实现方式：
答：
  1. 实现 getItemOffsets, 确定 vertical 或者 horizontal 的的分割线的高度或者宽度
  2. 在 onDraw 中确定需要画出的分割线的位置信息，并画到 画布 中即可；

  getItemOffsets()
  getItemOffsets()
  getItemOffsets()
        .
		.
		.
  getItemOffsets()  // 每个 childView 执行一次，onDraw 则只执行一次
  onDraw()

[Rect 类中 left、top、right、bottom 的理解](/home/linky/profile/ltrb.png)


2016年 09月 01日 星期四 15:43:45 CST

[学习 CardView 的使用](https://developer.android.com/reference/android/support/v7/widget/CardView.html)

[CardView 点击效果](http://blog.csdn.net/jdsjlzx/article/details/51243716) 
[another](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/1025/3621.html)


===

2016年 09月 02日 星期五 09:46:28 CST

1. 给 cardView 添加监听事件


2016年 09月 02日 星期五 10:11:10 CST

定制自动提示 fail

2016年 09月 02日 星期五 10:30:32 CST

[android 自定义图形开发](http://keeganlee.me/post/android/20150830)
===

[代码中设置粗体](http://blog.csdn.net/cw2004100021124/article/details/12453623)

[在代码中设置 TextView 的 drawableXXX 的方法](http://www.lai18.com/content/804043.html)

1. drawable = getDrawable
2. drawable.setBounds()
3. tv.setCompoundDrawables(l,t,r,b);

2016年 09月 02日 星期五 13:58:24 CST

[添加购买按钮的点击效果，包括文本和背景颜色](http://www.cnblogs.com/xdindex/p/4567426.html)

[为 RecyclerView 添加分割线](http://www.jianshu.com/p/4eff036360da)

Q：在 RecyclerView 中的 ItemView 添加 background="@drawable/selector_"
后点击没有反应的解决方法：添加 `android:clickable="true"` 属性
[参考](https://gist.github.com/brucetoo/925f8b7cbc60af121886)


2016年 09月 02日 星期五 16:59:56 CST

关于屏幕适配的小发现：
  如果 LinearLayout 是一个根布局，那么不能在其中写 PaddingTop/Bottom/Left/Right 属性，否则不生效，可以在 子View 中添加相应的 marginTop/Bottom/Left/Right 即可
  






















