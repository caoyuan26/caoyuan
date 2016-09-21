#Git教程
 
###一、Git简介

1.1. Git的诞生
1.2.集中式的vs分布式
###二、安装Git

###三、创建版本库
	
###四、时光穿梭机	
4.1版本回退
4.2工作区和暂存区
4.3管理修改
4.4撤销修改
4.5删除文件
###五、远程仓库
5.1添加远程仓库
5.2从远程库中克隆

###六、分支管理
6.1创建与合并分支
6.2解决冲突
6.3分支管理策略
6.4Bug分支
6.5Feature分支
6.6多人协作
###七、标签管理
7.1创建标签
7.2操作标签
###八、使用GitHub
###九、自定义Git
9.1忽略特殊定义符
9.2配置别名
9.3搭建Git服务器
  ##十、总结

>###1、Git简介

Git是什么？

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

Git有什么特点？简单来说就是：高端大气上档次！

>####1.1 Git的诞生

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。


>####1.2 分布式 VS 集中式

* 集中式
SVN - CVS - ClearCase(IBM 收费) - VSS(微软)

* 分布式
git - BitKeeper(促使git诞生) - Mercurial - Bazaar

目前集中式常用的SVN, 分布式常用git

集中式

集中式版本控制系统, 版本库需要集中的放到一台服务器上, 在工作时, 用自己的电脑从中央服务器上将目前最新内容下载到本地, 实现效果后再讲内容推送到中央服务器.

* 缺点

1.中央服务器崩溃, 所有人都干不了活
2.网络带宽会影响文件下载和上传速度

分布式

分布式版本控制系统压根没有”中央服务器”这个东西, 每个人的电脑都是一个完整的版本库, 这样工作的时候并不需要网络. 多人协作, 在合并作品的时候, 只需将自己的内容传给对方, 对方既可以看到你修改的内容. 同时, git提供强大的分支, 可以将项目拆分, 使项目更加安全.

**注意** 

git虽然没有”中央服务器”, 但常常找出一台电脑来充当”中央服务器”, 不过其作用是为了方便交换, 因为, 协作的两个人不在同一个局域网, 或者其中一人电脑未开启等特殊情况.

* 优点

安全性极高, 即便自己的电脑坏了, 只需要从别人的电脑上重新clone一个版本库即可
强大的分支, 可以将一个大项目拆分成若干小功能来实现, 实现后再合并

###安装git(Linux)

1.在终端输入 git 查看git信息(如果没有安装会有下方的友好提示)

	```
	$ git
	The program 'git' is currently not installed. You can install it by typing:sudo apt-get install git
	```

2.如果没有安装, 在终端输入`sudo apt-get install git` 安装

**注意:** 

老一点的Debian或Ubuntu Linux，要把命令改为`sudo apt-get install git-core`，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把`GNU Interactive Tools`改成`gnuit，git-core`正式改为git。

>###3、创建版本库

版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

在一个有足够权限的地方创建空文件夹

在终端使用命令: 

	```
	$git init
	git initInitialized empty Git repository in /Users/michael/learngit/.git/
	```

这时git参考就建立好了, 而且是一个空仓库, 此时文件夹下会多一个.git隐藏文件, 它是来跟踪仓库变化的, 不要随意改动这个文件.
将内容放到版本库

1.git add fileName
2.git commit -m "info"

	```
	$ git add readme.md

	$ git add git_study.md

	$ git commit -m "add 2 files."
	```

**说明:** 

`git add` 告诉 git 我要加入某个文件, `git commit`告诉 git 内容可以放入版本库了, `git commit`后的 -m ‘xxx’ 参数的意思是这次提交做了哪些改动, 强烈建议写上, 因为用不了多久你就会忘了曾经做了什么. 因为`git commit` 一次可以提交多个文件, 所以可以先通过add多个文件, 然后`commit`一次提交.

>###4、时光机穿梭

* 在终端使用命令`git status`查看那些文件被改动, 以及那些文件将要被commit提交

* 在终端使用命令`git diff`查看文件被改动了什么

>###4.1版本回退

如果在修改文件过程中出现了什么错误, 需要回退到就版本, 怎么办呢?

在终端使用命令`git log`查看提交历史

	```
	commit f384b35e6c614ac5444efd0167e29fee66c9c37d
	Merge: c65e7a0 2a0f55c
	Author: caoyuan <2675142924@qq.com>
	Date:   Wed Sep 21 15:46:03 2016 +0800
	
	    merge with no-ff
	
	commit 2a0f55c64f68abb7cb69547063330821a3a0df39
	Author: caoyuan <2675142924@qq.com>
	Date:   Wed Sep 21 15:35:31 2016 +0800
	
	    add merge
	
	commit c65e7a0f684587adce36c2f972de7fb4ce53cd69
	Merge: 28d8785 71dbe9d
	Author: caoyuan <2675142924@qq.com>
	Date:   Wed Sep 21 14:58:04 2016 +0800
	```

如果觉得内容太多, 可以使用命令git log --graph --pretty=oneline --abbrev-commit 查看

	```
	yuan@yuan:~/learngit$ git log --pretty=oneline --abbrev-commit
	f384b35 merge with no-ff
	2a0f55c add merge
	c65e7a0 conflict fixed
	28d8785 & simple
	71dbe9d AND simple
	fc62eb2 brach test
	4c51d94 remove test.txt
	1ee3747 add test.text
	5895409 add cao
	9a97047 git track changes
	440c6b3 understand how stage works
	5396aed append GPL
	21c867f add 3 file
	9c6ce9f add 1 file
	```
**说明:** 
前面的一大串数字是commit id, 和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示.

上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
```
yuan@yuan:~/learngit$ git reset --hard HEAD^
HEAD is now at c65e7a0 conflict fixed
```
**注意:**
 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

>###4.2工作区和暂存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

* 工作区

工作区可以简单的理解为是git仓库目录下内容.

* 暂存区

回顾一下, 在将内容提交到仓库时候, 需要先使用`git add`一下, 此时这个add其实是吧内容提交到`stage`暂存区, 在执行commit的使用才会将stage暂存区中的内容提交到工作区.

`git add`命令将文件提交到缓存区
![20160921133228815.jpg](http://upload-images.jianshu.io/upload_images/2665727-48cc6f11eb90f748.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

先来看名词解释。

#####工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：

working-dir

#####版本库（Repository）

工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

**git-repo**

分支和HEAD的概念我们以后再讲。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：**

第一步：是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步：是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，`git commit`就是往master分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对readme.txt做个修改，比如加上一行内容：

	```
	Git is a distributed version control system.
	Git is free software distributed under the GPL.
	Git has a mutable index called stage.
	```

然后，在工作区新增一个LICENSE文本文件（内容随便写）。

先用git status查看一下状态：
	```
	$ git status
	On branch master
	Changes not staged for commit:
	 (use "git add <file>..." to update what will be committed)
	(use "git checkout -- <file>..." to discard changes in working directory)
	
	   modified:   readme.txt
	
	 Untracked files:
	   (use "git add <file>..." to include in what will be committed)
	
	   LICENSE
	no changes added to commit (use "git add" and/or "git commit -a")
	```
Git非常清楚地告诉我们，readme.txt被修改了，而LICENSE还从来没有被添加过，所以它的状态是Untracked。

现在，使用两次命令git add，把readme.txt和LICENSE都添加后，用git status再查看一下：

	```
	$ git status
	On branch master
	Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)
	 new file:   LICENSE
	 modified:   readme.txt
	
	```
现在，暂存区的状态就变成这样了：

git-stage

所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

	```
	$git commit -m "understand how stage works"
	[master 27c9860] understand how stage works
	 2 files changed, 675 insertions(+)
	 create mode 100644 LICENSE
	```
一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

	```
	$ git status
	On branch master
	nothing to commit (working directory clean)
	```
现在版本库变成了这样，暂存区就没有任何内容了：
 ```
git-stage-after-commit
```
###小结

暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。

没弄明白暂存区是怎么回事的童鞋，请向上滚动页面，再看一次。
