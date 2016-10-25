
2016年 10月 24日 星期一 09:55:02 CST

1. 直播暴力测试；
2. 添加崩溃日志上传功能库；
   [crashlytics](http://try.crashlytics.com/sdk-android/)
3. 下载 IDEA14
4. 上传用户机型信息等；


2016年 10月 24日 星期一 10:18:54 CST

多个工作区切换快捷键：
```
CTRL + ALT + 上下左右
```

2016年 10月 24日 星期一 11:34:35 CST

be familiar with fabric


About C In ubuntu:

[以下三个问题参考博客](http://blog.csdn.net/JQ_AK47/article/details/51786041)
Q1: 如何创建可执行文件？
答：没有动态和静态或链接库时：
```
gcc -o bin src.c
```
此时会生成可执行文件 bin

```
./bin 
```

Q2: 如何创建静态库？
答：
第一步：将 .c 文件编译为 .o 文件；
提示找不到 .h 文件的解决方法：
1. 加入 -I 选项，指明头文件路径；
2. 加入 include 路径；
```
C_INCLUDE_PATH=.
export C_INCLUDE_PATH
```

命令：
```
gcc -c -I ./ hello.c
```

第二步：用 ar 命令将 .o 文件转换为 .a 文件，成为静态库
```
ar cr libmyhello.a hello.o
```

Q3: 如何创建动态库？
答：
第一步，创建 .o 文件
```
gcc -c -fPIC hello.c
```
第二步，将 .o 文件转换为 .so 文件
```
gcc -shared -fPIC -o libmyhello.so hello.o
```

Q4: 如何链接静态库和动态库？
链接静态库：
1. 加入 -L 选项，指明静态库地址；
```
cc -o main main.c -L . -lmyhello
## or
gcc -o main main.c -L . -static -lmyhello 
```
2. 加入 library 路径；
```
LIBRARY_PATH=.
export LIBRARY_PATH
```
命令：
```
gcc -o main main.c -lmyhello
```

链接动态库：
三种方法解决找不到动态库的问题：
1. 将 .so 文件复制到 /usr/lib 和 /lib 目录下
2. 若 .so 放在 非 lib 目录下，那么需要将新目录加入 共享库配置文件
   `/etc/ld.so.conf` 然后执行 ldconfig
3. 在 shell 中执行
```
export LD_LIBRARY_PATH=/usr/local/mysql/lib:$LD_LIBRARY_PATH
```
或者在 /etc/profile 中执行
```
LD_LIBRARY_PATH=.
export LD_LIBRARY_PATH
```

最后执行命令
```
./bin
```
即可

答：Linux下类库主要有静态库和动态库两种库。其中，静态库在程序连接的时候
会自动的连接到程序里，所以一但编译完成，静态库也就不需要了。静态库通常
以.a结尾。例如：libutil.a libuuid.a libz.a等。而动态库在程序编译时并不
会被连接到目标代码中，而是在程序运行时才被载入，因此在程序运行时还需要
动态库存在。通常以.so结尾。如：libz.so。因此，静态库相对于共享库来说有
更高的效率但是也要消耗更多的空间。

2016年 10月 24日 星期一 16:31:48 CST





