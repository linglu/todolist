

2016年 09月 02日 星期五 17:35:43 CST

1. 开始直播页面的布局

新建 Activity
新建 activity_layout
运行查看效果

2016年 09月 05日 星期一 10:02:41 CST

1. 运行 微信登录和支付 demo；
2. 了解其原理并提供给 Ryan 测试；
3. 

2016年 09月 05日 星期一 11:21:04 CST

流程：
1. 请求 code
2. 用 code + AppId + AppSecret 请求 access_token
3. 获取 token 后请求其他资源

第一步：请求 code
```
final SendAuto.Req req = new SendAuth.Req();
req.scope = "snsapi_userinfo";
req.state = "wechat_sdk_demo_test";
api.sendReq(req);
```

说明：

1. [scope](https://open.weixin.qq.com/cgi-bin/showdocument?action=doc&id=open1419317851&t=0.14929091593137778#scope)

目前支持一下两个：snsapi_base，snsapi_userinfo
```
{ 
"access_token":"ACCESS_TOKEN", 
"expires_in":7200, 
"refresh_token":"REFRESH_TOKEN",
"openid":"OPENID", 
"scope":"SCOPE",
"unionid":"o6_bmasdasdsad6_2sgVt7hMZOPfL"
}
```

2. state 请求后原样返回，用于防止 csrf 攻击

返回参数说明：
ErrCode    *ERR_OK* 同意
           *ERR_AUTH_DENIED* 拒绝
		   *ERR_USER_CANCEL* 取消
code       仅在 ERR_OK 时有效
state      原样返回
lang       语言
country    国家

第二步：获取 code 后，请求获取 access_token
```
https://api.weixin.qq.com/sns/oauth2/access_token? \
appid=APPID \
&secret=SECRET \
&code=CODE \
&grant_type=authorization_code
```

以上参数全部为必填

返回示例：
```
{ 
"access_token":"ACCESS_TOKEN", 
"expires_in":7200, 
"refresh_token":"REFRESH_TOKEN",
"openid":"OPENID", 
"scope":"SCOPE",
"unionid":"o6_bmasdasdsad6_2sgVt7hMZOPfL"
}
```
返回字段说明：

>* refresh_token：用于用户刷新 *access_token*
>* openid : 授权用户唯一标识
>* unionid：当且仅当该移动应用已获得该用户的userinfo授权时，才会出现该字段

由于 access_token 的有效期目前为2个小时，比较短，当 access_token 超时后，
可以使用 refresh_token 进行刷新，刷新结果有两种：

1. 若 access_token 已超时，会获取一个新的
2. 若 access_token 未超时，会刷新超时时间

refresh_token 的有效期为 30 天，当其失效后，需要用户重新授权

*使用 refresh_token 刷新 token 的方法*

使用如下接口：
```
https://api.weixin.qq.com/sns/oauth2/refresh_token? \
appid=APPID& \
grant_type=refresh_token& \
refresh_token=REFRESH_TOKEN
```

说明：
>* grant_type 填 refresh_token
>* refresh_token 填第二步获取到的 refresh_token

正确的返回：
```
{ 
"access_token":"ACCESS_TOKEN", 
"expires_in":7200, 
"refresh_token":"REFRESH_TOKEN", 
"openid":"OPENID", 
"scope":"SCOPE" 
}
```

第三步：通过 access_token 调用接口

前提：
>* 1. access_token 有效且未超时；
>* 2. 微信用户已授权给第三方应用帐号相应接口作用域(scope)

Q：什么是 scope
答：代表用户授权给第三方的接口权限，经过用户授权，获取到
相应 access_token 后方可对接口进行调用。


===

2016年 09月 05日 星期一 14:03:26 CST

[具体接入步骤：](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=1417751808&token=&lang=zh_CN)

1. 导入 jar 包
2. 添加权限
```
<uses-permission android:name="android.permission.INTERNET"/> 
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/> 
```

3. 使用
(1) 注册到微信
要使你的程序启动后微信终端能响应你的程序，必须在代码中向微信终端注册你的id
```
IWXAPI api;
api = WXAPIFactory.create(this, APP_ID, true);
api.registerApp(APP_ID);
```

(2) 发送请求或者响应到 微信

`boolean sendReq(BaseReq req)`
`boolean sendResp(BaseResp resp)`

(3) 接收微信请求及返回值，三个步骤

1. 在包名目录下新建 wxapi 目录，并在其中新增一个 WXEntryActivity 类。
   并在 manifest 中新增 exported 属性为 true

2. 实现 IWXAPIEventHandler 接口，发送的请求将回调到 onReq 方法，发送的
   响应将回调到 onResp 方法
   
3. 在 WXEntryActivity 中将接收到的 intent 及实现了 IWXAPIEventHandler 接口
   的对象传递给 WXAPI 接口的 handleIntent 方法。可以在 WXEntryActivity 中
   的 onNewIntent 方法中回调 `api.handleIntent(getIntent(), this)`
   
===

2016年 09月 05日 星期一 14:43:15 CST

开始完成登录功能；

查看 keystore 签名信息

`keytool -list -v -keystore debug.keystore -storepass android`

===

2016年 09月 05日 星期一 15:42:21 CST

研究 随心播 app 中的获取直播列表接口

url：
http://182.254.234.225/sxb/index.php?svc=live&cmd=list

参数：(json 格式)
{"pageIndex":0,"pageSize":20}

在线 post 请求
http://coolaf.com/

返回结果分析：

```
{
	"data": {
		"totalItem": 13,
		"recordList": []
		},
    "errorCode": 0,
    "errorInfo": ""
}
```

recordList 中的元素格式如下：
```
 {
	"createTime": 1473061414,
	"title": "2元_255102312",
	"cover": "http://121.40.111.180:8092/OgoWwwU9SRwvE4br6s0hDaFo1eTm.png",
    "lbs": {
		 "longitude": 0,
		 "latitude": 0,
		 "address": ""
		 },
	"host": {
		"uid": "443444101",
		"avatar": "http://121.40.111.180:8092/9SRwvE4br6s0hDaFo1eTm.png",
		"username": "栗子老师"
		 },
    "admireCount": 0,
	"chatRoomId": "255102312",
	"avRoomId": 255102312,
	"timeSpan": 27,
	"watchCount": 1
	},
```

Suixinbo 中使用到的字段：
  host.uid
  host.username
  host.avatar
  avRoomId
  watchCount
  admireCount
  lbs.address
  
  
2016年 09月 05日 星期一 17:27:51 CST

**Important Info**

登录使用 TLSLoginHelper 中的 TLSPwdLogin 方法，
传入参数：UserName.toString(), password.getBytes(), TLSPwdLoginListener

  onPwdLoginSuccess(TLSUserInfo tlsUserInfo)
    登录成功后可以获得以下字段信息：
	   tlsUserInfo.identifier
	   getUserSigFromIdentifier(identifier)
	拿到 identifier 和 userSig 后
	   TIMUser user = new TIMUser();
	   user.setAccountType(accountType)
	   user.setAppIdAt3rd(sdkAppId)
	   user.setIdentifier(identify)
	   TIMManager.login(APPID,user,userSig,callback{
	      onError - loginFail
		  onSuccess - 成功后
		  1. 获取房间号 roomNum
		  2. 保存 identifier 等信息到 AvConfig
		  3. 使用 AvConfig 实际初始化 AVSDK
		  最后 jumpToHomeActivity
	   })
    
  onPwdLoginReaskImgcodeSuccess
  onPwdLoginNeedImgcode
  onPwdLoginFail - Log.e()
  onPwdLoginTimeout - Log.e()
  
**Important Info**

  进入直播界面后：EnterLiveHelper
  
  joinLive(int roomNum)
    joinImChatRoom(roomNum)
	  TIMGroupManager.getInstance().applyJoinGroup(roomNum, "reason", callback)
        onError() - 要么已经是成员了，要么失败，退出房间
		onSUccess()
		  joinAVRoom(roomNum)
		    // 初始化聊天室
			getConversation(GROUP, chatRoomId)
			setMessageListener(msgList -> parseIMMessage(msgList));
  

**Important Info**

2016年 09月 05日 星期一 19:11:37 CST

**搭建聊天功能**

1. 使用托管模式注册功能；
2. 使用托管模式登录功能；
3. 申请进入聊天室功能；
4. 发送聊天信息功能；

  
2016年 09月 06日 星期二 09:25:24 CST

按：MVP 层中，View 层有个 基类或者接口 BaseView，P 层有个基类或者接口
Presenter。Fragment/Activity 继承 BaseView，并实现其中固定的方法，P 层
实现 Presenter 并实现其中固定的方法，在 P 层中包含 Model 层的对象，通过
Dagger 进行依赖注入。在 View 层中获取 Presenter 可以通过 Dagger 注入，
再使用 set 方法将 BaseView 设置入其中，具体业务动作在 Presenter 中使用
Model层的对象实现，再通过 BaseView 的子类将界面变化显示在 View 层中。


2016年 09月 06日 星期二 09:52:37 CST

用户名注册流程

Q：有两个概念：tlsLogin 和 imLogin 是什么意思和区别？

tlsLogin - 直接登录时调用，调用成功后接着调用 imLogin
tlsLogin 用于登录到 TLS 帐号系统，imLogin 则用于登录到 IM 系统

tlsLogin 成功后会获取到 userSig 和 identifier，再使用这两者登录 IM 系统

2016年 09月 06日 星期二 10:40:23 CST

注册

开始进入 聊天接口请求阶段

2016年 09月 06日 星期二 14:43:14 CST

[学习如何在 emacs 中使用 w3m](http://wideaperture.net/blog/?p=3240)

1. 安装以下文件包
>* cvs
>* autoconf
>* libgc-dev
>* libncurses5-dev

2. 安装 w3m
3. 安装 emacs-w3m
4. Point Emacs to the New Mode
```
(add-to-list `load-path "~/emacs-w3m/")
(require 'w3m-load)
```

[emacs-w3m 快捷键](http://kongll.github.io/2015/04/24/Emacs-w3m-%E6%93%8D%E4%BD%9C%E5%BF%AB%E6%8D%B7%E9%94%AE/)


2016年 09月 06日 星期二 17:22:31 CST

开始总结 clean architecture + MVP + dagger + retrolambda 架构的要点

2016年 09月 06日 星期二 17:44:14 CST

[Dagger](http://www.jianshu.com/p/cd2c1c9f68d4)

Inject + Module(Provides) 提供注入对象，Component 是一个桥梁，一端是
Inject + Module(Provides)，提供的对象，另一端是目标类中的依赖对象

Inject 用于注解自己实现类的构造方法，Module 则用于提供已经存在的类，例
如 android framework 层提供的 Context、ThreadExecutor 或者第三方类库中
的类，例如 OkHttp 等

Component 之间可以依赖，从而共享其中 Module 中提供的类实例对象。

创建类实例有两种方法，通过 Inject 注解和通过 Module 创建，这两者有优先
级之分，Component 会首先从 Module中查找类实例，若找到则停止查找 Inject
维度。

### Qualifier限定符
在同一维度下，例如 Inject 维度下，同一个类有多个构造函数，注入器
（Component）应该选用哪种呢？此时 Qualifier 注解派上了用场。
Qualifier（限定符）就是解决依赖注入迷失问题的。

2016年 09月 06日 星期二 21:05:19 CST

### app 中 Component 职责的划分：
>* 要有一个全局的 Component，负责整个App 的全局类实例
>* 每个页面对应一个 Component，比如每个 Activity/Fragment 对应一个 Component

### dagger2 中真正创建单例的方法：
>* 在 Module 中定义创建全局类实例的方法；
>* ApplicationComponent 管理 Module；
>* 保证 ApplicattionComponent 只有一个实例；

###Scope Singleton 的作用
>* 更好地管理 ApplicationComponent 和 Module 之间的关系；
>* 若 ApplicationComponent 和 Module 的 Scope 是不一样的，则在编译时会报错；

按：几点发现：
1. 没有 Scope 的 Component 不能依赖有 Scope 的 Component；
   有 Scope 的 Component 可以依赖没有 Scope 的 Component；

2. 
Component <- Module 
Component <- TargetClass 

Module 中 provides 的类和 TargetClass 没有关系，两者只与 Component 有关
系，Component 中的 Scope 数量 应该 >= 后两者中的 Scope 数量，且应该包含

###Dagger2对目标类进行依赖注入的过程
step1：查找 Module 中是否存在创建该类的方法；
step2：若存在，查看该方法是否存在参数；
  2.1：若存在，重复 step1
  2.2：若不存在，直接初始化，一次依赖注入到此结束
step3：若不存在，则查找 Inject 注解的构造函数，看构造函数是否存在参数
  3.1：若存在，重复 step1
  3.2：若不存在，直接初始化，依赖注入结束

2016年 09月 06日 星期二 19:15:08 CST

[android 下的 md5 加密](https://www.mkyong.com/java/java-md5-hashing-example/)

2016年 09月 06日 星期二 19:53:38 CST

开始整理接口

ubuntu shell MD5 命令
`$ echo -n ’123456′ | md5sum`

[学习使用 Insomnia](https://insomnia.rest/documentation/environment-variables/)
POST 请求的参数是通过 Params 标签下的 key/value 值来定义和传递的


2016年 09月 07日 星期三 10:08:09 CST

9：00 ～ 今，完善上述 **Scope Singleton 的作用** 和 **Dagger2对目标类进
行依赖注入的过程**

下面理清 HasComponent 的用法：
1. 在 Activity 中实现 HasComponent<XXXComponent>，并对外提供相应的 component；
2. 在 Fragment 中获取到 component 之后，执行 inject() 方法注入依赖；




















