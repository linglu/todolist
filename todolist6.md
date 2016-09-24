

2016年 09月 07日 星期三 10:59:03 CST

调用课时列表接口，并且将其会显至界面，用户点击后，进入聊天室，
完成进入聊天室流程

2016年 09月 07日 星期三 11:22:21 CST

[Fragment 状态保持的问题](http://www.cnblogs.com/kissazi2/p/4116456.html)


2016年 09月 07日 星期三 14:16:19 CST

继续开始课时逻辑

[学习fastjson相关内容](https://github.com/alibaba/fastjson/wiki/Android%E7%89%88%E6%9C%AC)

分析完成 Clean-Architecture 

2016年 09月 07日 星期三 16:47:18 CST

开始根据 Clean-Architecture 的思路进行项目的改造和完善


项目改造进行到 Subscriber 这一步 2016年 09月 07日 星期三 18:30:17 CST


===


2016年 09月 08日 星期四 08:56:38 CST

[学习 Retrofit 相关内容](http://square.github.io/retrofit/)

Retrofit 使用三部曲：

```
public interface GithubService {
  @GET("users/{user}/repos")
  Call<List<Repo> listRepos(@Path("user") String user);
}
```

```
Retrofit retrofit = new Retrofit.Builder()
  .baseUrl("")
  .build()
  
GithubService service = retrofit.create(githubService.class);
```

```
Call<List<Repo>> repos = service.listRepos("octocat");
```

details

1. method：GET/POST/PUT/DELETE/HEAD
2. replacement holder：mehtod 中的占位符，在参数列表中必须在注解
   @Path() 中使用相同的字符串，例如

   @GET("group/{**id**}/users")
   Call<List<User>> groupList(@Path("**id**") int groupId);

3. Request Body
   ```
   @POST("users/new")
   Call<User> createUser(@Body User user);
   ```
   
4. Form Encoded and Multipart
5. Header Manipulation
```
@Headers("Cache-Control: max-age=640000")
@GET("widget/list")
Call<List<Widget>> widgetList();
```

```
@Headers({
    "Accept: application/vnd.github.v3.full+json",
    "User-Agent: Retrofit-Sample-App"
})
@GET("users/{username}")
Call<User> getUser(@Path("username") String username);
```

headers do not override each other.
```
@GET("user")
Call<User> getUser(@Header("Authorization") String authorization)
```

6. Synchronous vs. Asynchronous

  On Android, callbacks will be executed on the main thread. 

7. Converters
  built-in converters
  
  [Gson](https://github.com/google/gson): com.squareup.retrofit2:converter-gson
  [Jackson](http://wiki.fasterxml.com/JacksonHome): com.squareup.retrofit2:converter-jackson
  [Moshi](https://github.com/square/moshi/): com.squareup.retrofit2:converter-moshi
  [Protobuf](https://developers.google.com/protocol-buffers/): com.squareup.retrofit2:converter-protobuf
  [Wire](https://github.com/square/wire): com.squareup.retrofit2:converter-wire
  [Simple XML](http://simple.sourceforge.net/): com.squareup.retrofit2:converter-simplexml
  
8. Custom Converters
  Create a class that extends the `Converter.Factory` class
  
Done 2016年 09月 08日 星期四 09:58:50 CST

2016年 09月 08日 星期四 10:18:42 CST

单例的最佳实践


2016年 09月 08日 星期四 12:33:02 CST

完成了 Service 的构建，下午开始实际的接口调用操作

和 Simon、Ryan 讨论问题，面试一位 Java 工程师

2016年 09月 08日 星期四 18:28:57 CST

[如何在 Module 中使用 productFlavor](http://stackoverflow.com/questions/24307596/how-can-i-add-flavors-in-a-module-with-android-studio)

**Important**
===

在 presentation 的 build.gradld 中添加
`compile project(path: ':data', configuration:'wideDebug')`
表示引用了 data Module中的 wideDebug 版本，其对应的 BuildConfig 中的变量也引用
wideDeubg 这个 Flavor 的，所以每次只需修改此处的 configuration 即可。
例如如果 localDebug 中的 BuildConfig 包含本地服务器的 URL 地址，
wideDebug 包含远程服务器的 URL 地址，那么只需将 wideDebug 切换为 localDebug
即可切换 data Module 中对应的 URL 值。
**Important**
===

2016年 09月 08日 星期四 19:10:59 CST



2016年 09月 09日 星期五 09:41:02 CST

[给 Retrofit 接口输出打日志信息](http://www.tuicool.com/articles/6zIvQbb)
[another](http://blog.csdn.net/u013164293/article/details/51811930)

手机 ip 和 服务器 ip 地址问题

[有空试试 stetho](http://www.tuicool.com/articles/BF3aIzm)


2016年 09月 09日 星期五 17:54:13 CST

调试成功接口并提交代码，下面开始进入聊天室的内容








