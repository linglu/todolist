
2016年 10月 15日 星期六 11:34:37 CST

现在开始做课程介绍功能，

包括登录和未登录


2016年 10月 17日 星期一 11:07:19 CST

[对 retrofit HttpException 的解释](http://bytes.babbel.com/en/articles/2016-03-16-retrofit2-rxjava-error-handling.html)

* Exceptions with class retrofit2.adapter.rxjava.HttpException are of
  kind RetrofitError.Kind.HTTP. This means your call returned a non
  2XX status code.
  
* Exceptions with class java.io.IOException are of kind
  RetrofitError.Kind.NETWORK and RetrofitError.Kind.CONVERSION. This
  means something went wrong with your call or (de)serialization.
  
* All other exceptions are of kind RetrofitError.Kind.UNKNOWN

2016年 10月 17日 星期一 13:43:15 CST


===

2016年 10月 18日 星期二 09:19:37 CST

1. 个人中心 已购买课程点击进入介绍课程页面；
2. 对于已购买且到了直播时间的课程可以进入直播页面；
3. 

2016年 10月 18日 星期二 09:23:09 CST

先提交当前内容，然后发布，然后开始解决相关的 bug

1. 新建一门直播课程；
2. 进入直播页面；
3. 解决相关的 bug；


2016年 10月 18日 星期二 15:36:36 CST

下面开始调试 build.gradle 以配置 apk 命名和 versionCode 和 versionName

2016年 10月 18日 星期二 16:19:54 CST

下面开始做手机适配问题

新的一：尽量使用 support.v4.Frgament而不是 系统自带的 Fragment













