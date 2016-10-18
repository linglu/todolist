
2016年 09月 28日 星期三 09:15:28 CST

写转正申请书

2016年 09月 28日 星期三 11:15:46 CST 先告一段落

下面开始布局 UI 界面

行业选择界面

支付界面 at 2016年 09月 28日 星期三 18:06:30 CST

done at 2016年 09月 28日 星期三 18:46:57 CST

=== 

2016年 09月 29日 星期四 09:40:47 CST

[partnership on AI](https://techcrunch.com/2016/09/28/facebook-amazon-google-ibm-and-microsoft-come-together-to-create-historic-partnership-on-ai/)

接下来开始布局其他界面 UI

1、支付成功界面
2、支付失败界面
3、评价界面
4、查看评价界面

2016年 09月 29日 星期四 10:44:30 CST

趁着使用 Observable 实现倒计时功能，学习相关的内容知识

[Scheduler](https://mcxiaoke.gitbooks.io/rxdocs/content/Scheduler.html)

按：

1. 有些操作符有有默认的执行线程，例如 delay 操作符，默认执行在
   computation 调度器上，如果需要自己指定执行的 Scheduler，需要在操作号
   之后，再通过执行 observeOn() 来指定，否则会被操作符的默认 Scheduler
   覆盖掉。

2. 当料想中会发射 n 个数据，结果只发射了 k < n 个时，很有可能是因为遇到
   了错误，执行了 onError，此时不会继续发射数据了。


=== 

2016年 09月 29日 星期四 14:32:56 CST

[查看显卡硬件信息](https://www.sysgeek.cn/graphics-card-information-linux/)

`>$ lspci -vnn | grep VGA -A 12`
`>$ lshw -C display`

2016年 09月 29日 星期四 15:05:29 CST

Q：在使用 repeatWhen 时，
第一种：onNext() -> call() -> onNext() -> call() -> ... -> onComplete()
第二种：onComplete()

第二种的意思是，没有执行 onNext，直接执行到 onComplete() 中去了

经过测试，发现有如下规律：

1. notificationHandler 返回的 Observable 不是 Void 类型的时，则直接执行了
   onComplete() 方法；
2. notificationHandler 返回的 Observable 是 Void 类型时，则不断重复执行
   onNext() 方法，效果跟 repeat() 一样；
3. notificationHandler 返回的 Observable 里面有转化逻辑时，比如
   zipWith().flatMap() 时，将根据里面的转化逻辑决定重试次数；
   
[一篇值得参考的文章](http://blog.danlew.net/2016/01/25/rxjavas-repeatwhen-and-retrywhen-explained/)


1. 当 Observable 收到 onCompleted() 方法时，repeat() 会重订阅；
2. 当 Observable 收到 onError() 方法时，retry() 会重订阅；

但是这些简单的版本有些事情办不到，例如延迟订阅和根据检测到的错误类型来
判断是否需要重订阅，此时 repeatWhen 和 retryWhen 便派上用场了

重试或者重复逻辑是通过一个叫做 notificationHandler 的方法来提供的；

1. Func1
2. 输入是一个 Observable<Throwable>
3. 输出是一个 Observable<?>

我们先看一下第三个参数 Observable<?>，它决定了重订阅是否发生，如果是它
释放了 onError 或者 onCompleted，那么重订阅不发生，如果释放了 onNext()
那么重订阅便发生了

input 是一个 Observable<Throwable>，每当 source 调用 onError(Throwable) 时
便会释放一个。换句话说，每当你决定是否重试时会被触发。

如果我们只想在 Throwable 为 IOException 时重试，可以如下实现：
```
source.retryWhen(errors -> errors.flatMap(error -> {
    // For IOExceptions, we  retry
    if (error instanceof IOException) {
      return Observable.just(null);
    }

    // For anything else, don't retry
    return Observable.error(error);
  })
)
```

每个错误都被映射了，所以我们或者返回 onNext(null)（此时会触发重订阅）或
者 onError(error)（此时避免触发重订阅）

有几点需要注意的：

>* repeatWhen 和 retryWhen 类似，一个对应 onCompleted，一个对应 onError

>* notificationHandler 对于每个 subscription 只会被调用一次；

>* output Observable 必须使用 input Observable 作为它的源，换句话说，你
>  不能像这样使用 
```
retryWhen(errors -> Observable.just(null))，不仅仅是因为这样不能工作，
而且它完全打破了你的序列
```

>* input Observable 只会在终端事件（onCompleted for repeatWhen /
>  onError for retryWhen）触发，而不会收到任何 onNext 通知。所以你不能
>  通过检测释放的数据来决定是否重新订阅，如果你想这么做，可以考虑使用
>  takeUntil() 来截获 stream

使用场景：
1. 定期获取数据: repeatWhen + delay
```
source.repeatWhen(completed -> completed.delay(5, TimeUnit.SECONDS))
```

由于 notificationHandler 在释放 onNext 之前，延迟了 5s，所以实现了周期
性获取数据的效果

2. flatMap + timer
```
source.repeatWhen(o -> o.flatMap(o -> Observable.timer(5, TimeUnit.SECONDS)));
```

3. zip + range
```
source.retryWhen(errors -> errors.zipWith(Observable.range(1, 3), (n, i) -> i));
```

最终结果是，每个 error 会和 range 的一个输出配对，所以：

zip(error1, 1) -> onNext(1)
zip(error1, 2) -> onNext(2)
zip(error1, 3) -> onNext(3)
onCompleted()

Combine the above for limited retries with variable delays:

```
source.retryWhen(errors ->
  errors
    .zipWith(Observable.range(1, 3), (n, i) -> i)
    .flatMap(
	retryCount -> Observable.timer(
	(long) Math.pow(5, retryCount), TimeUnit.SECONDS)));
```

按：在实践过程中发现，最好不要从外部传入变量到 Observable 内部，会发生
一些奇怪的事情，跟料想的不太一样。


2016年 09月 30日 星期五 09:20:37 CST

支付成功界面、支付失败界面，done

2016年 09月 30日 星期五 09:20:58 CST

下面开始布局评价界面

done at 2016年 09月 30日 星期五 10:14:59 CST

下面开始布局 

查看评价界面

done at 2016年 09月 30日 星期五 11:47:45 CST

接下来先将代码提交至 git 服务器；
然后开始做 提示框、加载框等内容

下午先把修改的接口和后台对一对

[使用 Shadowsocks 翻墙](http://www.jianshu.com/p/20d55422f83c)

2016年 09月 30日 星期五 15:36:57 CST

由于后台的不可控性，有必要开始做分支操作；

以一个稳定版本为基准，当有新的需求进来时，或者来自自己计划中的，或者来
自其他方面的，通过开分支的方式解决，解决完后，要么合并进入主干，要么丢弃；

下面开始学习 git 分支的相关内容知识

[git详解之三 Git 分支](http://www.open-open.com/lib/view/open1328069889514.html)

因为
    Git 保存的不是文件差异或者变化量，而只是一系列文件快照
    Git 提交时，会保存一个提交对象(内容快照指针、Meta 信息、父对象指针)

课程信息的 date 格式化显示

2016年 09月 30日 星期五 18:39:51 CST



    






























