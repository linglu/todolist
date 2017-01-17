

2017年 01月 03日 星期二 09:14:07 CST

1. 使用不销毁的方式实现回放的全屏和非全屏的切换；
  （1）将布局文件写在同一个 .xml 文件中，全屏布局使用 include 方式
      外层使用 RelativeLayout，然后里面两大布局，一大布局用于非全屏，
	  一大布局用于全屏；
  （2）当界面切换时，除了 PlayView 之外，其他的控件都重定向到对应的控件当中，
      PlayerView 切换显示方向；
  （3）从全屏切换到非全屏，首先重定向控件，然后切换 PlayerView 显示方向；

2. 聊天内容处理


2017年 01月 04日 星期三 09:26:57 CST

1. 聊天内容接入；

(1) 先获取聊天记录内容，然后映射到 Map<Long, List<>> 中，
(2) 获取到每一段视频的 startTime，然后在 onPlayEvent 回调函数中，
    查询 Map 中的数据，若获取到，添加显示到聊天记录中，
(3) 当拖动 SeekBar 结束时，清空 Adapter 中的 List 数据；
(4) 全屏和非全屏的 RecyclerView 共用一个 Adapter，依次保证聊天内容
    的同步显示；


2017年 01月 05日 星期四 10:07:20 CST

一、 几种情况

1.1 顺序播放
  1.1.1 顺序播放
  1.1.2 顺序跳集
  
1.2 往前拖动
  1.2.1 同一集内的往前拖动
  1.2.2 往前不同集数跳集

1.3 往后拖动
  1.3.1 同一集内的往后拖动
  1.3.2 往后不同集数跳集
  
  // 处理顺序播放的问题；
  // 往前和往后拖动的逻辑相同；
  
  ```
    mSeekBar.setOnSeekBarChangeListener(new OnSeekBarChangeListener() {
	  void onSeekBarChange() {
        // 通过 timestamp 获取单条消息
	    getMsgByTimestamp();
	  }

	  void onStopTracking() {  // 处理拖动时的问题
	  // 获取代码段
	    getMsgList(lessonId, startTime, true)
	  }
	});	
  ```

  // 处理跳集播放的情况；
  ```
    view.setOnClickListener(v - {
	    if (mCurPlaySeg != index) {
		  getMsgList(lessonId, startTime, true);
		}
	})
  ```

  ```
	if (msgType.equals("FlagMsg") && mFlagMsgCount % 2 == 0 && isFinish == 1) {
	  mFlagMsgCount++;
	  getMsgList(lessonId, startTime, false);
	}
	
	getPlaybackMsgByTimeStamp();
  ```

  // 重新加载聊天列表的情况
  1. 往前、后拖动进度条； // SeekBar 监听
  2. 跳集；  // setOnClickListener(v -> {})
  3. 顺序播放时，遇到 FlagMsg 标识；  // 
  
二、MsgList 请求成功后的处理方式

  1. 放入 HashMap 中；
  2. 每次获取到一个消息后，从 HashMap 中删除；
  3. 如果是拖动、换集造成的，则清空之前的 HashMap 数据
     所以在请求列表时，还需要加一个参数，用于标识是否需要清空之前的数据；
  
三、遇到的问题

  1. 空值的判断，比如获取每秒的消息时；done 
  2. 聊天信息清空的时机；
     2.1 拖动进度条时；
     2.2 切换集数时；
  3. 聊天内容的显示顺序；  done 
  4. 更新内容后，自动滑动到底部；  done 
  5. 更多消息的显示和消失时机；
  
  

  
  
