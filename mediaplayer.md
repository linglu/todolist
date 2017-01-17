
2016年 10月 31日 星期一 11:08:30 CST

1. 单箭头表示同步操作调用，双箭头表示异步操作调用；
[mediaplayer_state_diagram](/home/linky/todolist/pic/mediaplayer_state_diagram.gif)


* 当 new 了一个 MediaPlayer 或者 调用 reset() 方法之后，处于 idle 状态；
   调用了 release() 方法后，处于 END 状态；这两者之间的状态就是
   MediaPlayer 的生命周期；
   
* 新 new 的一个 MediaPlayer 和 调用了 reset 方法之后的 MediaPlayer 之间
  有微妙的差别，当处于 idle 状态时，调用以下方法是程序性错误
  getCurrentPosition(), 
  getDuration(), 
  getVideoHeight(), 
  getVideoWidth(), 
  setAudioStreamType(int),
  setLooping(boolean), 
  setVolume(float, float), 
  pause(), 
  start(), 
  stop(), 
  seekTo(int), 
  prepare()
  prepareAsync()
  
* 新 new 的 MediaPlayer 如果调用以上方法，不会回调
  OnErrorListener.onError()，而调用了 reset() 方法进入 idle 状态的
  MediaPlayer 会回调 OnErrorListener.onError() 方法从而进入 Error state
  
* 当不用 MediaPlayer 时，需要调用 release() 方法，如果该方法调用失败，
  将导致后续的实例回退到软件实现或者一起失败。一旦 MediaPlayer 进入
  END 状态，将不可能再次进入其他状态；
  
* 通过 new 的方式创建的 MediaPlayer 将处于 idle 状态，而调用 create 方
  法创建的则将处于 prepared 状态；
  
* 当出现错误时，例如不支持格式、分辨率太高等，内部 player engine 将调用
  OnErrorListener.onError() 方法，如果事先注册了的话，一旦错误发生，将
  进入 ERROR 状态，此时可调用 reset 使其重新进入 idle 状态。如果在不合
  法的状态调用 prepare()、prepareAsync()、setDataSource()将抛出
  IllegalStateException 异常以阻止编程错误；

* 调用 setDataSouce() 方法，MediaPlayer 将从 idle 转化到 initialized 状
  态；如果在 idle 状态之外的其他状态调用 setDataSource() 将抛出
  IllegalStateException 异常；

* 在重载的 setDataSouce 方法注意 IllegalArgumentException 和
  IOExceptio 异常是个好的编程实践
  
* MediaPlayer 只有进入 Prepared 状态才能执行播放操作，有两种方法进入
  Prepared 状态，一种是 prepare()，当这个方法返回时，则进入了Prepared
  状态，还有一种是 prepareAsync() 方法，调用此方法将首先进入 preparing
  状态，然后当准备好其他工作后，player 引擎将回调
  OnPreparedListener.onPrepared() 方法，此时也进入了 prepared 状态
  
* Preparing 状态是短暂的，在此期间执行的其他操作都是未定义(undefined)

* 当处于 *Prepared* 状态时，可以通过调用相应的方法来设置 player 的属性，
  例如 audio/sound volume, screenOnWhilePlaying
  
* 调用 start() 方法，进入 *started* 状态，isPlaying() 可用于检测是否处于该状态；

* 当处于 started 状态时， internal player engine 将回调
  OnBufferingUpdateListener.onBufferingUpdate() 方法以跟踪缓存情况；
  
* 处于 started 状态时调用 strat() 方法将没有什么效果；

* 播放状态，从 started 到 pause 是异步的，状态的切换需要花费一些时间；
  在 pause 状态调用 pause() 方法没有效果
  
* 调用 stop() 方法将使 MediaPlayer 从 Started, Paused, Prepared or
  PlaybackCompleted 状态进入 stopped 状态
  
* 进入 stoped 状态后，playback 不能 start， 直到调用了 preapre() 和
  prepareAsync() 重新进入 Prepared 状态
  
* playback 位置可以通过 seekTo(int) 方法调整，虽然该方法立即返回，但是
  实际上需要花费一些时间，当 seek 操作完成后，player engine 将回调
  OnSeekComplete.onSeekComplete() 方法

* 可以通过方法 getCurrentPosition() 来获取当前的播放位置；

* 当播放结束时，如果 looping mode 设置为了 true，那么 MediaPlayer 将仍
  然处于 Started 状态，如果 looping mode 设置为了 false，Player Engine
  将回调 OnCompletion.onCompletion() 方法，此时 MediaPlayer 进入
  PlaybackCompleted 状态，此时可以调用 start() 方法来重新播放音视频；
  
  

  



  


