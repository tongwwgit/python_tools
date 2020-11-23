### tmux

tmux ls命令可以查看当前所有的 Tmux 会话。
tmux attach命令用于重新接入某个已存在的会话。

$ tmux attach -t 0    使用会话编号

$ tmux attach -t <session-name>  使用会话名称

最简单的流程：
新建会话tmux new -s my_session。
在 Tmux 窗口运行所需的程序。
按下快捷键Ctrl+b d将会话分离。
下次使用时，重新连接到会话tmux attach-session -t my_session。

或者
tmux
Ctrl+b d
tmux attach -t 0

* tmux 做屏幕拆分
  * Ctrl-B +% 竖直拆分屏幕（两个 Shell 分别位于左右）
  * Ctrl-B +" 水平拆分屏幕（两个 Shell 分别位于上下）
  * Ctrl-B +O 切换到另一个 Shell
  * Ctrl-B +X 关闭当前的 Shell
  * Ctrl-B +！ 关闭所有的 Shell

### 文件操作命令

* ls | wc -w  查看文件夹下多少文件

* du 会显示指定的目录或文件所占用的磁盘空间。

  du -h --max-depth=1  列出的最大目录层数为1

#### 环境变量

* 在 shell 中执行程序时，shell 会提供一组环境变量。
* export 可新增，修改或删除环境变量，供后续执行的程序使用
* 环境变量：$PATH：决定了shell将到哪些目录中寻找命令或程序，PATH的值是一系列目录，以冒号分隔；当您运行一个程序时，Linux在这些目录下进行搜寻编译链接。
* echo $PATH  #列出所有环境变量
* 添加新的变量到PATH:  export PATH=/mnt/lustre/tongwenwen/anaconda3/bin:$PATH
* LD_LIBRARY_PATH是Linux环境变量名，该环境变量主要用于指定查找共享库（动态链接库）时除了默认路径之外的其他路径。
* echo  $HOME: 查看home主目录