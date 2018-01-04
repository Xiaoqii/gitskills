## git

###### 前言

- 本文档是学习[缪雪峰的git教程](http://t.cn/zQ6LFwE)后，做的笔记，方便回头复习。
- 本笔记主要记录了教程中所有的命令、一些代码段和一些常见问题。
- [《Pro Git》](http://dwz.cn/2Sm61P)



##### 一、创建版本库

第一步，创建版本库，选择一个合适的地方，创建空目录：

```
$ cd /d		#进入D盘
$ mkdir learngit	#创建仓库文件夹
$ cd learngit	#进入文件夹
$ pwd	#显示当前目录
/Users/michael/learngit #目录位于的地址
```

第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：

```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

```
$ git status #命令可以让我们时刻掌握仓库当前的状态
$ git diff #顾名思义就是查看difference
```

**小结**

- 初始化一个Git仓库，使用`git init`命令。
- 添加文件到仓库的暂存区，使用`git add <文件名>`，可以反复多次添加多个文件。
- 使用命令`git commit`，将文件提交到分支上。

- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。
- 所有的版本控制系统，其实只能跟踪文本文件的改动。




##### 二、增删改查

`git status`  ***命令***  可以让我们时刻掌握仓库当前的状态

```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   gitnote.md

no changes added to commit (use "git add" and/or "git commit -a")

```

`git diff`  ***命令***  可以查看修改内容。

`git log`  ***命令***  可以查看从最近到最远的提交日志，显示的信息太多可以加上`--pretty=oneline`参数。

```
$ git log --pretty=oneline
3c1181174db9f2aa6ebc6ab64f13c9bcc35debaf (HEAD -> master) wrote a read file
a197e22b9f6754e58dc6ba9001b2a20073a71698 git note
d1e266ae159e8a10a494a18e11e80ce8f1e9b93f wrote a readme file

#d1e2····9b93f是commit id（版本号）
```

`git reset`  ***命令***  可以把当前版本回退到某一个版本。

```
$ git reset --hard HEAD^
HEAD is now at ea34578 add distributed
```

`git reflog`  ***命令***  用来记录你的每一次命令。

`git diff HEAD -- <file>`  ***命令***  可以查看工作区和版本库里的最新版本区别



```
$ git reflog
3949594 (HEAD -> master, origin/master) HEAD@{0}: commit: wu ta
af746dd HEAD@{1}: commit: 2018/01/04
412d2d2 HEAD@{2}: checkout: moving from master to master
412d2d2 HEAD@{3}: commit: AND simple
74fe18c HEAD@{4}: checkout: moving from new_branch to master
```

`git checkout -- file`  ***命令***  可以丢弃工作区的修改，命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令。

```
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

```

`git rm <文件名>`  ***命令***  删除该文件。

**小结**

- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。
- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。
- 现在，你又理解了Git是如何跟踪修改的，每次修改，如果不`add`到暂存区，那就不会加入到`commit`中。
- 撤销修改：
  - 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
  - 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。


- 命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。



##### 三、远程仓库

```
$ ssh-keygen -t rsa -C "youremail@example.com" #创建SSH Key
```

```
$ git remote add origin git@github.com:kingwc2017/learngit.git
```

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

```
$ git push origin master
```

```
$ git clone git@github.com:kingwc2017/gitskills.git
```

**小结**

- 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

  关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

  此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；



##### 四、分支管理 

