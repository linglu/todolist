
[参考](https://learnxinyminutes.com/docs/elisp/)

(+ 2 2)

>* setq 函数定义变量
(setq var "value")

>* insert 函数，显示到控制台
(insert "value")
(insert var)
(insert "" "")

>* 定义函数 和 执行函数
(defun funcname () ())
(funcname)

>* progn 函数，将连续执行的语句放在一起
(progn
  ()
  ()
  ()
)

>* let 函数，1. 给变量赋值；2. 将连续执行的语句放在一起
(let ((var "value"))
  ()
  ()
  ()
)

>* format 函数，使用占位符格式化
(format "Hello %s" value)

>* 获取用户输入，与用户交互
(read-from-minibuffer "Enter your name: ")

>* 定义数组，单引号 ' 表示取字面意义，不执行
(setq list-of-names '("" "" ""))

>* car 去数组第一个元素
(car list-of-names)

>* cdr 取数组从第二个到最后一个
(cdr list-of-names)

>* push 将新元素插入数组第一个位置
(push "First Element" list-of-names)

>* mapcar 遍历数组
(mapcar 'hello list-of-names)

>* while 语句
(while ()
  ()
)

>* switch-to-buffer-other-window 跳转到另一个 buffer 区
`(switch-to-buffer-other-window "*test*")`

>* erase-buffer 清空当前缓冲区
(erase-buffer)

>* other-window 进入指定窗口
(other-window 1)


