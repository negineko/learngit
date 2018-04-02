==参考地址==:
[廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000)


# 目录
[toc]

==写在前头==<br>
下文中所有前面带"$"字符的操作是在git bash中运行的.
git bash在安装git后即可启动.window版本可在开始菜单查找git bash运行.
默认也会添加到邮件菜单.也可以邮件菜单运行<br><br>
==运行时git命令时需把工作目录移动到版本库.即有.git的目录下==
<br>
本文为[廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000)中的摘要,顺序也与廖雪峰git教程一致.有必要时查阅原地址查看更相信信息.



# 安装git
## linux和ubuntu版本

### sudo apt-get install git

## windows版本
https://git-scm.com/downloads

### $ git config --global user.name "Your Name"
### $ git config --global user.email "email@example.com"
```
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git
仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
```

# 创建版本库
### $ git init 
在当前目录下创建版本库

### $ git add filename 
把文件添加到版本库的工作区.一次可添加多个文件(然后才提交)

### $ git commit -m "annotation"
把工作区的文件提交到版本库.-m 内写明本次提交的注释
```
$ git commit -m "annotation"
[master (root-commit) cb926e7] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
 ```

### $ git status
命令可以让我们时刻掌握仓库当前的状态<br>
把文件用add命令提交到工作区之后可以用git status命令查看状态,可以显示出于上次提交相比被修改了的文件的清单.显示为:<br>
```
modified:   changedfile
```
			
### $ git diff
顾名思义就是查看difference(差异)
```
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```

# 版本回退
### $ git log
查看日志.
```
$ git log
commit 3628164fb26d48395383f8f31179f24e0882e1e0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 15:11:49 2013 +0800

    append GPL

commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 14:53:12 2013 +0800

    add distributed

commit cb926e7ea50ad11b8f9e909c05226233bf755030
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 19 17:51:55 2013 +0800

    wrote a readme file
```

### $ git log --pretty=oneline
返回简易日志
```
$ git log --pretty=oneline
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
```
你看到的一大串类似3628164...882e1e0的是==commit id（版本号)==

### $ git reset --hard HEAD^
在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

### $ git reset --hard version id
```
$ git reset --hard 3628164
HEAD is now at 3628164 append GPL
```
回到版本号的版本,==回退版本后悔丢失最新版本的内容,需要回复时需要通过id来找回(但这个id将不会再被记录,这次的终端关了之后就找不到了.)==

### $ git reflog
```
$ git reflog
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
```
Git提供了一个命令git reflog用来记录你的每一次命令：
	
# 工作区和暂存区
[参考地址](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013745374151782eb658c5a5ca454eaa451661275886c6000)

# 撤销修改
### $ git checkout -- file
丢弃工作区的修改
实际上是用工作区的file和版本库的file做对比,把工作区中的file替换成版本库的file

如果已经写入到暂存区
### $ git reset HEAD readme.txt
```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt
```
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。<br>
然后再用checkout命令丢弃工作区修改即可。

# 删除文件
### $ git rm file
```
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
[master d17efd8] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
 ```
 删除版本库中的file
 
 # 远程仓库
 [参考地址](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)
 
### $ git clone 
```
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.
```
注意把稳重的git@github.com:michaelliao/gitskills.git改成目标的地址
进行这一步之前需要在github上注册ssh_key,见<a href = "#远程仓库">远程仓库</a>

# 分支管理
## 创建与合并分支
[参考地址](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000)

常用命令:
### $ git checkout -b dev
```
$ git checkout -b dev
Switched to a new branch 'dev
```
创建并切换到dev分支,等效于下面2条命令
```
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```
### $ git branch
```
$ git branch
* dev
  master
```
查看当前分支用"*"标识的是当前分支.
### $ git merge dev
```
$ git merge dev
Updating d17efd8..fec145a
Fast-forward
 readme.txt |    1 +
 1 file changed, 1 insertion(+)
 ```
把dev的内容合并到master分支上
### $ git branch -d dev
```
$ git branch -d dev
Deleted branch dev (was fec145a).
```
删除分支dev

##解决合并冲突
当合并产生冲突的时候会产生如下结果:
```
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```
此时用git status查看冲突文件.
```
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```
再查看冲突的文件:
```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
```
git会自动为你标识出冲突的位置.把不需要的内容删除即可提交&合并.
用git log --graph命令可以看到分支合并图。

## 分支管理策略

通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，==会丢掉分支信息==。

#### 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，==平时不能在master上干活==；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：
![image](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

## bug分支
Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

### $ git stash
```
$ git stash
Saved working directory and index state WIP on dev: 6224937 add merge
HEAD is now at 6224937 add merge
```
储存现工作区状态.

### $ git stash list
```
$ git stash list
stash@{0}: WIP on dev: 6224937 add merge
```
查看储存列表<br>
<hr>
用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了
### $ git stash pop
```
$ git stash pop
# On branch dev
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   hello.py
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   readme.txt
#
Dropped refs/stash@{0} (f624f8e5f082f2df2bed8a4e09c12fd2943bdd40)
```

你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：
```
$ git stash apply stash@{0}
```
强制删除分支
```
$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 756d4af).
```
## 多人协作
远程仓库的默认名称是origin,
要查看远程库的信息，用git remote：
```
$ git remote
origin
```
或者，用git remote -v显示更详细的信息：
```
$ git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)
```

推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
```
$ git push origin master
```
如果要推送其他分支，比如dev，就改成：
```
$ git push origin dev
```

因此，多人协作的工作模式通常是这样：

1. 首先，可以试图用git push origin branch-name推送自己的修改；

2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

3. 如果合并有冲突，则解决冲突，并在本地提交；

4. 没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。
<hr>

查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

# 标签管理
### git tag <name>
就可以打一个新标签：
```
$ git tag v1.0
```
对之前的修改打标签
### $ git tag v0.9 commit id
```
git tag v0.9 6224937
```
commit id<a href="#版本回退">查看方法</a>
或者:
```
$ git log --pretty=oneline --abbrev-commit
6a5819e merged bug fix 101
cc17032 fix bug 101
7825a50 merge with no-ff
6224937 add merge
59bc1cb conflict fixed
400b400 & simple
75a857c AND simple
fec145a branch test
d17efd8 remove test.txt
```

查看所有标签.
### $ git tag
```
$ git tag
v0.9
v1.0
```

### $ git show <tagname>
查看标签信息：
```
$ git show v0.9
commit 622493706ab447b6bb37e4e2a2f276a20fed2ab4
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 11:22:08 2013 +0800

    add merge
```

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
```
$ git tag -a v0.1 -m "version 0.1 released" 3628164
```
删除标签

### $ git tag -d <tagname>
```
$ git tag -d v0.1
Deleted tag 'v0.1' (was e078af9)
```
如果要推送某个标签到远程，使用命令
### $ git push origin <tagname>：
```
$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
 * [new tag]         v1.0 -> v1.0
```


如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
```
$ git tag -d v0.9
Deleted tag 'v0.9' (was 6224937)
```
然后，从远程删除。删除命令也是push，但是格式如下：
```
$ git push origin :refs/tags/v0.9
To git@github.com:michaelliao/learngit.git
 - [deleted]         v0.9
```
# 参与github上的项目
<a href = "https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137628548491051ccfaef0ccb470894c858999603fedf000">参考地址</a><br>
<a href="https://github.com/">GitHub</a>
# 自定义git
<a href="https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137621280731812dec22ecc9b44f4b2ca1c680f181a5b000">参考地址</a>