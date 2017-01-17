
2016年 10月 24日 星期一 17:23:40 CST

[git tag 操作](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)

1. 含附注的标签 -a (annotated) 

```
git tag -a v1.4 -m 'my version 1.4'
```

2. 查看 tag 信息
```
git show v1.4 
```

2016年 10月 25日 星期二 10:52:14 CST

1. 为 首页 RecyclerView 添加 Header;
done

直播所有问题的根源：在退出房间时没有做收尾操作

Q1: chat room view is null 的问题
A：在进入房间时，通过语句 
TIMManager.getInstance().addMessageListener(msgListener);
设置了回调操作，而 TIMManager 是全局单例，所有每次进入房间时都进行了
addMessageListener 操作，这样的话，便添加了多次，从而回调了多次，
只有此次的回调 ChatRoomView != null，其他情况则都为 null，所以弹出了
那个 Toast 提示

Q2：收尾都需要做哪些操作？
答：待续，参考 随心播 app

2016年 10月 25日 星期二 19:47:25 CST

* 观看直播时发现的一些问题：
1. 竖屏聊天时，聊天内容过长时，需要留出右边距；done
2. 标题和全屏图标，5s 后应该自动消失，而不是一直停留在那，横屏类似；
3. 最多显示聊天内容条数；  done 
4. 让聊天内容被输入法顶上去；

5. 将聊天字体加大一个 px 试试；

2016年 10月 26日 星期三 09:28:33 CST

1. 加入重新链接服务器功能；

1. 理清 RecyclerView、Adapter、LayoutManager 之间的关系；

2016年 10月 26日 星期三 09:48:24 CST

1. 先解决重音的问题；
2. 


presentation 下的 lib/*.jar 包的用途：

聊天相关 jar 包
```
libs/bugly_1.3.0_imsdk_release.jar
libs/imsdk.jar
libs/mobilepb.jar
libs/qalsdk.jar
libs/tls_sdk.jar
libs/wup-1.0.0-SNAPSHOT.jar
libs/soload.jar
```
libammsdk ： 用于微信登录
txrtmpsdk ： 用于直播


2016年 10月 26日 星期三 14:06:10 CST

在 ubuntu 下编译运行 C++ 程序，需要使用 g++ 程序
```
sudo apt-get isntall g++
```

2016年 10月 26日 星期三 20:27:16 CST

1. 更换 .so 和 .jar 文件；
2. 修改 Activity 的 Theme；
3. 修改代码进入直播；
4. 测试；






