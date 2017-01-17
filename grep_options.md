
grep 

 -E --extended-regexp
 -F --fixed-strings
 -G --basic-regexp
 -P --perl-regexp
 
 Q: 这几种 regexp 之间有什么区别？
 
 -e PATTERN 匹配多个 PATTERN
 -f file 
 [出现的问题及解决方法](http://stackoverflow.com/questions/26754181/greps-invalid-range-end-bug-or-feature)
 
 -i --ignore-case  忽略大小写
 -v --invert-match 相反匹配
 -w --word-regexp  输出匹配整个单词的行
 -x --line-regexp  输出匹配整行的行
 
 -c --count  输出匹配的行数
 -L --files-without-match 输出没有匹配字符的文件名
 -l --files-with-matches  输出有匹配字符的文件名
 
 -m NUM --max-count=NUM 只输出匹配的前前 NUM 行
 -o --only-matching 只输出匹配的部分
 
 按：几个考虑的对象
 
 文件、行、词
 
 大小写、逆运算、行数、单词数
 
 精确匹配 (-w)、模糊匹配 (默认) 
 
 输出行前缀
 -b --byte-offset 输出匹配行的字节偏移
 -H --with-filename 为每个匹配打印文件名
 -h --no-filename 不为每个匹配输出文件名
 -n --line-number 输出每个匹配的行号
 -T --initial-tab 每个输出的匹配行前加入一个制表符，-H,-n 搭配使用
 
 按：
 文件、  行、  词
 文件名  行号  字节偏移
 
 格式化输出
 
 -A NUM --after-context=NUM  输出匹配行的后面 NUM 行，组间用 -- 分隔
 -B NUM --before-context=NUM 输出匹配行的前面 NUM 行，组间用 -- 分隔
 -C NUM --context=NUM 输出匹配行的前后 NUM 行
 
 -I 忽略二进制文件
 
 -D ACTION --devices=ACTION 如果输入文件是一个设备，FIFO 或者 socket，
  使用 ACTION 去处理他。默认情况下，ACTION 是 read，如果 ACTION 是
  skip，那么 devices 将被跳过
  
 -d ACTION --directories=ACTION 如果输入是一个目录，使用 ACTION 去处理
  他，默认情况下，ACTION 是 read，如果 ACTION 是 skip，那么跳过目录，如
  果 ACTION 是 recurse，递归遍历目录，类似 -r 选项
  
  限定搜索范围
 --exclude=GLOB
 --exclude-from=FILE
 --exclude-dir=DIR
 --include=GLOB
 
 递归搜索
 -r --recursive 只搜索出现在命令行的 符号链接
 -R --dereference-recursive 递归搜索所有 符号链接
 
 REGULAR EXPRESSIONS
 
 A regular expression is a pattern that describes a set of strings. 
   正则表达式是描述字符串集合的模式
 
 
 
 
 
 
 
 
 
 
 
 


 
