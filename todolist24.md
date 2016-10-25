
2016年 10月 24日 星期一 17:23:40 CST

[git tag 操作](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)


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







