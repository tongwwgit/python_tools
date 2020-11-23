#### Linux下面用命令如何运行.sh文件的方法

* 直接./加上文件名.sh，如运行hello.sh为./hello.sh【hello.sh必须有x权限】
* 直接sh 加上文件名.sh，如运行hello.sh为sh hello.sh【hello.sh可以没有x权限】



#### 其他操作命令

* 引用变量：$var 或${var}

* bash脚本中分号：单行语句一般要用到分号来区分代码块

* shell中#*,##*,#*,##*,% *,%% *的含义及用法        https://blog.csdn.net/jiezi2016/article/details/79649382

* set命令：显示系统中已经存在的shell变量，以及设置shell变量的新变量值

  linux脚本中使用 set -x就可以有详细的日志输出