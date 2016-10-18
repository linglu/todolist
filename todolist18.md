
2016年 10月 09日 星期日 10:37:21 CST

1. 与 IOS 调试直播流程；
2. 使用 git 分支进行项目管理；

2016年 10月 09日 星期日 11:43:44 CST

组合切换流程


2016年 10月 10日 星期一 09:20:20 CST

1. 创建分支
2. 完成页面布局操作
3. 合并分支
4. 从 git 服务器更新代码（并解决冲突，如果有的话）
4. 提交 code review
5. 提交到 git 服务器

2016年 10月 10日 星期一 09:33:00 CST

1. 创建分支，ui_conponent

todo :
1. 上周遗留的切图问题；
2. 登录页新增返回按钮；
3. 课程下架后点击操作问题；


关于课程结束的判断：

1. 在正常上课之外，比如 19：00 ～ 21：00 之外；
2. 直播网络不稳定；
3. 拖堂 若干分钟（此数据从后台获取）后，
   强制课程退出，此时发送一个课程结束消息给后台；

2016年 10月 10日 星期一 12:57:04 CST

下午尽快完成对话框内容，然后开始进行 Toast、当前无网络的判断等逻辑；

完成后，进行直播停止的检测工作等等

2016年 10月 10日 星期一 13:53:26 CST

[学习通过命令行连接或断开 VPN](http://askubuntu.com/questions/57339/connect-disconnect-from-vpn-from-the-command-line)

* 列出当前可用的连接
```
>$ nmcli con 
```

* 连接 uuid 为 $uuid 的 vpn
```
>$ nmcli con up uuid $uuid
>$ nmcli con up id $name
```

* 断开 uuid 为 $uuid 的 vpn
```
>$ nmcli con down uuid $uuid
>$ nmcli con down id $name
```

2016年 10月 10日 星期一 14:20:29 CST

完成 自动连接 vpn 的 shell 脚本，下面开始做其他界面布局操作

1. 完成 Toast 通用界面及显示；

2016年 10月 10日 星期一 16:24:59 CST

修改 Toast 样式

2016年 10月 10日 星期一 19:52:00 CST

下面开始优化首页的界面

2016年 10月 11日 星期二 09:16:12 CST

1. 配置公网 ip 地址访问接口；


2016年 10月 11日 星期二 10:21:55 CST

Q：如何运行 Android Studio 中的 lint 以显示警告信息？

[设置 lint 代码设置](http://www.jianshu.com/p/ba1ce1c1ae39)

2016年 10月 11日 星期二 17:46:27 CST

[Git如何获得两个版本间所有变更的文件列表](https://segmentfault.com/q/1010000000133613)

[分支切换时，对现有修改的处理方法](https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%82%A8%E8%97%8F%EF%BC%88Stashing%EF%BC%89)

储藏 - Stashing



























