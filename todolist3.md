

2016年 08月 29日 星期一 13:47:45 CST

1. 首页 -》 课程页 -》 直播页

>* Theme 使用 Theme.AppCompat.NoActionBar

>* 关于使用 AutoLayout 进行适配的一些发现：
  https://github.com/hongyangAndroid/AndroidAutoLayout
  
  1. 在根布局中，需要使用 AutoXXXLayout 控件，要么通过在 xml 中使用
     要么通过在 @Override public View onCreateView() 中进行复写和转化，
     子布局和子控件不变
	 
  2. 如果通过继承 布局控件来实现自定义控件，需要继承 AutoXXXLayout
  
  3. 对于其他继承系统的FrameLayout、LinearLayout、RelativeLayout的控件，
     比如CardView，如果希望在其内部直接支持"px"百分比化，可以自己扩展，
	 
	 
2016年 08月 29日 星期一 16:00:20 CST

关于 RxFragmentActivity: http://www.open-open.com/lib/view/open1448189551399.html

===

2016年 08月 30日 星期二 15:09:36 CST

Fragment 与 Activity 之间的关系

MainActivity:onCreate null

MainActivity:onCreate Bundle[{
    android:viewHierarchyState=Bundle[{
	    android:views={
		    16908290=android.view.AbsSavedState$1@2ce8159, 
			2131427395=android.view.AbsSavedState$1@2ce8159, 
			2131427396=android.view.AbsSavedState$1@2ce8159, 
			2131427397=android.support.v7.widget.Toolbar$SavedState@12c611e, 
			2131427398=android.view.AbsSavedState$1@2ce8159}}]}]

在 Activity 中，当 屏幕 切换时， saveInstanceState 并不为 Null，可以据
此判断是否发生屏幕切换等；


Q：如何模拟后台 Activity 被系统杀死回收，并再次创建？答：
答：[几种方法](http://www.androidyuan.com/post/android%E5%BC%80%E5%8F%91%E4%B8%AD%E6%A8%A1%E6%8B%9F%E7%B3%BB%E7%BB%9F%E5%86%85%E5%AD%98%E4%B8%8D%E8%B6%B3-%E5%BA%94%E7%94%A8%E9%87%8A%E6%94%BE%E7%9A%84%E6%83%85%E5%86%B5)
   
   1. 打开 DDMS，点击其上的 stop 按钮
   2. 使用命令：(将来可以提供给测试人员模拟测试)
   `adb shell am kill <package_name>`
   
   [This is different to `adb shell kill`](stackoverflow.com/questions/11365301/how-to-simulate-android-killing-my-process)
   
===

Activity 中有个 FragmentManager，内部维护 fragment 队列以及 fragment 事务的回退栈

[about fragment](http://blog.csdn.net/lmj623565791/article/details/42628537)

1. 方法 add(R.id.container, newFragment) 中的 R.id.container 的作用，一
   方面是告知 FragmentManager，此 fragment 的位置，另一方面是作为该
   fragment 的唯一标识，之后可以通过
   fm.findFragmentById(R.id.container)查找；

[屏幕旋转](http://blog.csdn.net/lintcgirl/article/details/51727569)

1. 任何 Configuration 的改变都会对 Activity 的界面造成影响，比如
   orientation、screenSize、字体大小、语言等，此时该 activity 先走了
   onPause、onStop、onDestroy，然后再执行 onCreate

2. 在 manifest 中给 activity 设置
`android:configChanges="orientation|screenSize|keyboardHidden"`的意思是，
屏幕旋转(orientation)、屏幕大小改变(screenSize)、键盘辅助功能改变
(keyboardHidden) 对该 activity 没有影响。

3. 在 android 3.2 (API Level 13) 及更高的版本中，如果需要捕获屏幕切换事
件，在 AndroidManifest.xml 中对应的 Activity 下面，除了在
android:configChanges 中添加 orientation 属性外，还需要添加 screenSize
属性，`android:configChanges="orientation|screenSize"`然后对应的
Activity 中的 onConfigurationChanged 方法才能得到回调，此时屏幕依旧会切
换，但是 activity 不会走 onPause、onStop、onDestroy 然后再执行
onCreate，而是直接回调了 onConfigurationChanged 方法。
(http://stackoverflow.com/questions/5620033/onconfigurationchanged-not-getting-called)

Q：如何禁止屏幕切换？
>* 在 manifest.xml 中进行如下配置
`android:screenOrientation="portrait"`
`android:screenOrientation="landscape"`

>* 在 Activity 代码中
`setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE)`
`setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT)`

Q：[DialogFragment 创建对话框](http://blog.csdn.net/lmj623565791/article/details/37815413)


Q：对 back stack 的理解，对 Activity 管理 back stack 的理解
 [Fragment 返回栈的管理](http://www.cnblogs.com/smyhvae/p/3983234.html)
 
FragmentTransaction 提供了一个 addToBackStack() 方法，可以将一个事务添加到返回栈中
```
FragmentManager fragmentManager =getFragmentManager();
FragmentTransaction transaction = fragmentManager.beginTransaction();
RightFragment rightFragment = new RightFragment();
transaction.add(R.id.right, rightFragment);
```
**transaction.addToBackStack(null);**

`transaction.commit(); `

在提交事务之前调用 FragmentTransaction 的 addToBackStack() 方法，一般传
入 null 即可

执行`transaction.replace(R.id.right, rightFragment);` 时，如果被替换的
Fragment 没有压入栈中，就会被销毁，在执行完 onDestroyView 后会继续执行
onDestroy() 和 onDetach() 方法

Note：
Fragment 的 back stack 由 Activity 管理；而 Activity 的返回栈由系统管理。

===
Q：FragmentTransaction 中的 commitAllowingStateLoss 方法的含义？
[Fragment Transactions和Activity状态丢失](http://blog.jobbole.com/66117/)
[英文版](http://www.androiddesignpatterns.com/2013/08/fragment-transaction-commit-state-loss.html)

1. onSaveInstanceState() 背后到底发生了什么？

  这个问题源于，这些 Bundle 对象在 onSaveInstanceState() 被调用时表示了
  一个 Activity 的快照，没有更多。这意味着当你在 onSaveInstanceState 之
  后调用 FragmentTransaction#commit()时， transaction 不会被记住，因为
  在第一个地方，它没有被记录为 Activity 状态的一部分。从用户的角度来来
  看，交易似乎被丢失了，从而导致意外的 UI 状态丢失。为了保护用户体验，
  Android不惜代价要避免状态丢失，所以就简单地抛出了异常。
  
  在 Honeycomb(3.0) 之前，activity 在 onPuase() 执行之后才能被 kill，这
  意味着 onSaveInstanceState() 紧挨着 onPause() 之前调用。但是从
  Honeycomb(3.0) 开始，activity 在 onStop() 之后才能被 kill，这意味着
  onSaveInstanceState() 紧挨着 onStop() 之前执行。
  
  在 Honeycomb(3.0) 以及之前的设备，每次 commit() 在
  onSaveInstanceState() 之后执行都会抛出 Exception 以提醒 developer 状
  态丢失发生了。然后这似乎对 Honeycomb(3.0) 之前的设备太严格了。于是
  Android 团队做了一个折中，让状态丢失发生在 onpause() 和 onStop() 之间。
  
  **如何避免**
  1. 当在 Activity 的生命周期方法中提交 transaction 时要小心。尽量在
     onCreate() 方法中调用。如果你的应用需要在 Activity 除了
     onCreate() 之外的生命周期方法中调用，那么要么在
     FragmentActivity#onResumeFragments() 要么在
     Activity#onPostResume() 方法中调用。这两个方法会保证在 Activity 已
     经恢复到它的原始状态之后才被调用，从而避免了状态丢失的可能性。
     [在 OnActivityResult 中执行 transaction 的一种处理方法](http://stackoverflow.com/questions/16265733/failure-delivering-result-onactivityforresult)
  2. 避免在异步回调方法中执行 transactions；
  3. 使用 commitAllowingStateLoss() 是最后一个方法；


2016年 08月 30日 星期二 20:43:04 CST

关于 onSaveInstanceState() 和 onRestoreInstanceState() 方法执行时机的探索

环境：
MI4, 6.0.1 MMB29M

按 Home 键时：
  onSaveInstanceState()
  
横竖屏切换时
  onSaveInstanceState()
  onCreate()
  onRestoreInstanceState()
  
执行 adb shell am kill <package_name> 时
  没有反应
  
===

2016年 08月 31日 星期三 09:20:55 CST

环境：
华为畅玩 4.4.2

按 Home 键时：
  onSaveInstanceState()
  
横竖屏切换：
  onSaveInstanceState()
  onCreate()
  onRestoreInstanceState()

执行 adb shell am kill <package_name> 时
  没有反应













  




