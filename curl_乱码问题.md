
curl "" 出现乱码的解决方法

使用 

`curl "" | iconv -f GB18030 -t utf-8`

该命令将 GB18030 的编码格式转化为 utf-8 的格式

出现 iconv: illegal input sequence at position 10263 的原因及解决[方法](blog.chinaunix.net/uid-20764167-id-3522067.html)
