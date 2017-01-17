
2016年 11月 02日 星期三 11:04:21 CST

[Android中关于日期时间与时区的使用总结](http://www.2cto.com/kf/201312/266908.html)

默认情况下，如果单纯使用 SimpleDateFormat 格式化一个 long 时间戳，将使
用本时区的时间，在中国，则为 +8，如果想消除这个影响，则可以通过
setTimeZone 设置其时区
