

上班至今 讨论本周任务 2016年 09月 12日 星期一 10:33:37 CST

2016年 09月 12日 星期一 10:46:22 CST 修改 ubuntu 输入法设置

[下面开始调试微信登录接口：](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=1417751808&token=6aa34ab7540b3555236fa318837fee5ef6f18e7b&lang=zh_CN)

1. 导入 jar 包：libammsdk
2. 添加权限
3. 开发步骤：
  1. 注册到微信
  api.registerApp(APP*ID);
  
  2. 发送请求或响应
  boolean sendReq(BaseReq req);
  boolean sendResp(BaseResp resp);
  
  3. 接收请求或者响应结果 -- 通过回调方式
  a. 在包名目录下新建 wxapi 目录，新增 WXEntryActivity 类，继承自 Activity；
  b. 在 Manifest.xml 中添加 exported 属性，设置为 true;
  c. 实现 IWXAPIEventHandler 接口，请求回调到 onReq，响应回调到 onResp；
  d. 传递给 IWXAPI 的 handleIntent 方法；
  
[微信登录接入步骤：](http://songyuanlin1101.lofter.com/post/30e704*3c2671f)

[微信授权过程中碰到的问题](http://www.cnblogs.com/andy2simple/p/4160004.html)
[another](http://blog.csdn.net/cs_li1126/article/details/49387539)


===

2016年 09月 13日 星期二 09:29:06 CST

[一个小坑](https://github.com/square/retrofit/issues/907)

Retrofit.Builder().baseUrl(URL)，此处的 url 需要以 '/' 结尾，
在具体接口路径中，不要以 '/' 开头，例如 @GET("path/to/res")
否则 baseUrl 中将只获取到 host 地址和端口后，后面的路径都将丢失

2016年 09月 13日 星期二 10:26:07 CST

关于 git 的几个发现：

本地 commit 后，code review 之前，
先使用 git pull 同步本地与远程仓库，
如果有冲突则解决冲突，然后再次 commit，
完了之后在 code review，
最后执行 arc land，将本地代码同步到远程；

上午完成了微信的登录功能，并提交到 git 服务器；

===
2016年 09月 13日 星期二 13:38:45 CST

调试聊天信息背景显示问题

2016年 09月 13日 星期二 15:48:42 CST

 user_id : U1AVEPRBF7X2JJZ3M330GGN, token : 46ddba27c7432b91708183c41a2ab311











