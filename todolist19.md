

2016年 10月 12日 星期三 09:12:13 CST

1. 完成购买流程；
2. 进入个人中心再进入直播；


接口的配置；

ProgressBar 放一放

2016年 10月 12日 星期三 10:27:57 CST

关于 微信登录 WXEntryActivity 的坑

调起微信登录后，再返回时，微信客户端会再次 startActivity，此时如果
WXEntryActivity 的 launchMode 不是 single 的话，将会再次创建一个 Activity
此时将会出现两个了

[singleTask](http://www.tuicool.com/articles/2qiAF3A)


[singleTask 和 newIntent 的问题](http://www.2cto.com/kf/201302/187348.html)

2016年 10月 12日 星期三 14:29:53 CST

[通过 Intent 传递类对象及优先考虑 Parcelable 的原因](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0104/2256.html)

找个时间将 LessonIntroActivity 修改为 CourseIntroActivity
找个时间将 request/lesson 修改为 request/course 







