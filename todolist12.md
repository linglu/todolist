emacs

2016年 09月 21日 星期三 15:30:16 CST

1. 面试一名 IOS 工程师
2. 下载 Terminal Emulator For Android 用于通过 tcpip 连接手机

[adb shell 命令](https://developer.android.com/studio/command-line/shell.html)

am - Activity Manager 命令
pm - Package Manager 命令

2016年 09月 21日 星期三 15:33:45 CST

按：

Android 界面包括：
>* 静态界面
  >* onMeasure、onLayout、onDraw
  >* android View 坐标系
>* 动画效果
  >* 补间动画(res/anim)、帧动画(res/drawable)、属性动画(res/animator，3.0后添加)
  >* 滑动
  >* 矩阵变换、矩阵运算
  
android 的输入方式：
>* 动作
  >* 点击、长按、手势
>* 输入类型
  >* 文字、语音、图片
  

Q：Android 的坐标系是怎样的？
答：Android 有两种坐标系，Android 坐标系和视图坐标系，[链接](http://www.jianshu.com/p/5b6e2d936a78)
1. Android 坐标系：以左上角为原点(0,0)，x 轴向右延伸正，y 轴向下延伸为正。
2. 视图坐标系：View 是一个二维矩形，所以需要四个数值来确定其位置

控件自身宽高：
getHeight()
getWidth()

View 自身坐标
getTop()    - View 自身顶边 相对于父布局的上边距
getLeft()   - View 自身左边 相对于父布局的左边距
getRight()  - View 自身右边 相对于父布局的左边距
getBottom() - View 自身底边 相对于父布局的上边距

关系：
getHeight() = getBottom() - getTop()
getWidth() = getRight() - getLeft()

MotionEvent 提供的方法，按：MotionEvent 反应的是点击事件，点击事件在屏
幕上中表示为一点，所以只需要两个数值，x、y 来确定其位置

getX() - 相对于所在控件的左边距
getY() - 相对于所在控件的上边距
getRawX() - 相对于整个屏幕的左边距
getRawY() - 相对于整个屏幕的上边距

Q：Android 一个应用在屏幕上的显示分区如何？
答：[链接1](http://blog.csdn.net/yanbober/article/details/50419117)、[链接2](http://crazyandcoder.github.io/2016/06/24/android%20%E8%87%AA%E5%AE%9A%E4%B9%89view%E7%B3%BB%E5%88%97%E2%80%94%E5%B1%8F%E5%B9%95%E5%9D%90%E6%A0%87%E7%9F%A5%E8%AF%86%E7%82%B9%E6%80%BB%E7%BB%93/)

从上到下：
>* 状态栏区域
>* 标题栏（ActionBar）区域
>* View 布局区域

应用程序 App 区域包括：标题栏（ActionBar）区域 + View 布局区域
屏幕区域：状态栏 + 应用程序 APP 区域

2016年 09月 21日 星期三 17:33:05 CST
开始阅读 LinearLayout 的 onMeasure 源码

阅读之前，搞懂相关的一些概念和知识，
放在 [ViewGroup.md](~/todolist/ViewGroup.md) 中

2016年 09月 21日 星期三 17:55:07 CST


===

2016年 09月 22日 星期四 10:41:01 CST

[学习滚动动画](http://www.jianshu.com/p/06d7d04772f8)

1. 实现 View 滑动的六种方法
>* layout()
>* offsetLeftAndRight() & offsetTopAndBottom()
>* LayoutParams
>* 动画
>* scrollTo & scrollBy 
>* Scroller

[Scroller 原理分析](http://blog.csdn.net/mr_liabill/article/details/49022721)

2016年 09月 22日 星期四 14:10:35 CST

[属性动画](http://www.jianshu.com/p/3f1405b48fad)

最重要的类：ObjectAnimator 

常用的可以直接使用的属性动画的属性值

translationX
translationY

rotation
rotationX
rotationY

PivotX
PivotY
控制 View 对象的支点位置，围绕这个支点进行旋转和缩放

alpha 
透明度，默认为 1，不透明

x
y
描述 View 对象在它容器中的最终位置

按：Res 下不同目录下的文件包含的根元素不同

anim/     - <set />
animator/ - <objectAnimator />
drawable/ - <selector />

>* ValueAnimator
>* 动画监听
>* 组合动画 AnimatorSet
>* 组合动画 PropertyValuesHolder
>* xml 中使用属性动画

2016年 09月 22日 星期四 15:28:59 CST

[关于动画，有空需要尝试](http://wiki.jikexueyuan.com/project/android-animation/1.html)

===

接下来开始按照没有动画的思路进行全屏代码实现

2016年 09月 22日 星期四 17:35:58 CST 实现完成

完成过程中的几个坑：
布局文件需要使用 dp，不能使用 px，否则由于 AutoxxxLayout 的存在，
否则通过 LayoutParam 设置全屏时有一些问题。有时间研究一下 
===

2016年 09月 22日 星期四 17:38:52 CST

开始着手，在全屏状态下右边拉出聊天框的问题

1. 当视频全屏时，设置显示区域也全屏

done

















