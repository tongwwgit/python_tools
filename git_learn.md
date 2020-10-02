### git 安装配置

windows下载gitbash。

git config 这个工具，可专门用来配置或读取相应的工作环境变量。

在 Windows 系统上，Git 会找寻用户主目录下的 .gitconfig 文件。主目录即 $HOME 变量指定的目录

```git
$git config
列出所有的选项

配置个人用户名和电子邮件
$ git config --global user.name "runoob"
$ git config --global user.email test@runoob.com
--global 更改的配置文件就是位于你用户主目录下的那个，以后所有的项目都会默认使用这里配置的信息

查看已有的配置信息
$git config -l
查看配置文件
$vim ~/.gitconfig
查看某个环境变量
$git config user.name
```

### git 工作区，暂存区，缓存区

* 工作区：就是你在电脑里能看到的目录。

* 暂存区：英文叫 stage 或 index。一般存放在 .git 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。

* 版本库：工作区有一个隐藏目录 .git，这个不算工作区，而是 Git 的版本库。

### git创建仓库

git init 初始化一个git仓库

```git
git init     #使用当前目录作为Git仓库,会在当前目录出现一个名为.git的目录
git init newrepo       #使用我们指定目录作为Git仓库。 
```

git clone 从现有的git仓库在拷贝项目

```git
git clone <repo>
git clone <repo> <directory>     #克隆到指定的目录
```

### git基本操作

1. git add  添加一个或多个文件到缓存区

   ```git
   git add [file1] [file2] ...
   git add .      #添加所有文件到缓存区
   ```

   

2. git status 命令用于查看在你上次提交之后是否有对文件进行再次修改。

   ```git
   git status -s  #使用 -s 参数来获得简短的输出结果
   ```


3. git diff  较文件在暂存区和工作区的差异。

4. git commit 命令将暂存区内容添加到本地仓库中。

   ```python
   git commit -m [message]    #-m 可以额外增加备注信息
   git commit -a  #-a 参数设置修改文件后不需要执行 git add 命令，直接来提交
   ```

   