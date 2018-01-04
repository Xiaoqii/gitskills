## git

​	此次学习git之前，一直在使用svn，这次使用缪雪峰老师的教程，做以下简单的笔记，方便回头查看。[git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

### 创建版本库

###### 第一步：

```
$ cd /d 
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
#进入你想创建仓库的文件夹
```

`pwd`命令用于显示当前目录。在我的Mac上，这个仓库位于`/Users/michael/learngit`。

###### 第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：

```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

```
$ git status #命令可以让我们时刻掌握仓库当前的状态
$ git diff #顾名思义就是查看difference
```

**小结**

- 要随时掌握工作区的状态，使用`git status`命令。
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。



### 文件的增删改查

`git log`命令显示从最近到最远的提交日志,如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数。

```
$ git log --pretty=oneline
3c1181174db9f2aa6ebc6ab64f13c9bcc35debaf (HEAD -> master) wrote a read file
a197e22b9f6754e58dc6ba9001b2a20073a71698 git note
d1e266ae159e8a10a494a18e11e80ce8f1e9b93f wrote a readme file
```

### 远程仓库

```
$ ssh-keygen -t rsa -C "youremail@example.com" #创建SSH Key
```

