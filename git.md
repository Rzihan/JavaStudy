# Git的简单使用

## 1、两个命令

```
$git config -- global user.name "your name"

$git config -- global user.email "your email"
```

## 2、创建版本库

### 2.1、创建空目录

```
$ mkdir learngit

$ cd learngit

$ pwd

/c/Users/Pan梓涵/learngit
```

pwd 命令用于显示当前目录。

### 2.2、通过`git init`命令把这个目录变成Git可以管理的仓库：

```
$ git init 

 Initialized empty Git repository in C:/Users/Pan梓涵/learngit/.git/
```

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的。

### 2.3、把文件添加到版本库

所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

#### 使用Windows的童鞋要特别注意：

千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载[Notepad++](http://notepad-plus-plus.org/)代替记事本，不但功能强大，而且免费！记得把Notepad++的默认编码设置为UTF-8 without BOM即可。

## 3、使用git的例子

#### 3.1、用命令git add告诉Git，把文件添加到仓库

`$git add readme.txt`

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功

#### 3.2、用命令git commit 告诉Git，把文件提交到仓库

```
$ git commit -m "wrote a readme file"
[master (root-commit) 60b2c7a] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。 

为什么Git添加文件需要add,commit 一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

```
$git add file1.txt

$git add file2.txt file 3.txt

$git commit -m "add 3 files"

```

![1531121413400](C:\Users\Pan梓涵\AppData\Local\Temp\1531121413400.png)

* 这是因为没有同时提交信息，即：git commit -m "这里是信息"，
* 即上面红色部分，添加就不会出现提示了，
* 上面的界面退出     输入命令 ：wq    即可

#### 3.3、小结

现在总结一下今天学的两点内容

初始化一个Git仓库，使用git init 命令。

添加文件到Git仓库，分为两步：

1. 使用命令git add<file>,注意，可反复多次使用，添加多个文件；
2. 使用命令git commit -m<message>,完成

## 4、时光机穿梭

#### 4.1、修改readme.txt文本的内容，然后使用git status命令查看运行结果

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

`	git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改 

#### 4.2、使用git diff查看具体修改了什么内容

```
$ git diff
diff --git a/readme.txt b/readme.txt
index d8036c1..013b5bc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
\ No newline at end of file
```

​	git diff顾名思义就是查看difference，可以从上面的命令输出看到，我们在第一行添加了一个distributed单词。

​	知道了对readme.txt作了什么修后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样 两步，第一步是git add;

`$ git add readme.txt`

​	同样没有任何输出。在执行第二部 git commit 之前，我们再运行git status看看当前仓库的状态

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

modified:   readme.txt
```

​	git status告诉我们，将要被提交的修改包括readme.txt，下一步，就可以放心地提交了：

```
$ git commit -m "add distributed"
[master dc9fea2] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
```

​	提交后，我们再用git status命令看看仓库的当前状态

```
$ git status
On branch master
nothing to commit, working tree clean
```

​	Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。

#### 4.3、小结

* 要随时掌握工作区的状态，使用git status命令
* 如果git status 告诉你又文件被修改过，用git diff可以查看修改内容。

## 5、版本回退

#### 5.1、使用git log命令显示从最近到最远的提交日志

```
$ git log
commit cb28dba4c0dcaf38664bfc49c7218d9903eac18c (HEAD -> master)
Author: zihanPan <470590444@qq.com>
Date:   Mon Jul 9 11:23:39 2018 +0800

append GPL

commit dc9fea23625ad3d645fd69c2d2e80d246006126c
Author: zihanPan <470590444@qq.com>
Date:   Mon Jul 9 11:12:04 2018 +0800

add distributed

commit 60b2c7a28506d25be8f00a6cd475beeb99e3c85a
Author: zihanPan <470590444@qq.com>
Date:   Mon Jul 9 10:05:03 2018 +0800

wrote a readme file
```

​	如果嫌输出信息太多，看得眼花缭乱的，可以试试加上 --pretty=oneline 参数

```
$ git log --pretty=oneline
cb28dba4c0dcaf38664bfc49c7218d9903eac18c (HEAD -> master) append GPL
dc9fea23625ad3d645fd69c2d2e80d246006126c add distributed
60b2c7a28506d25be8f00a6cd475beeb99e3c85a wrote a readme file
```

​	需要友情提醒的是，你看到的一大串类似1090adb...的是commit id（版本号），和SVN不一样，Git的commit id不是1,2,3....递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示嫩？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1,2,3……作为版本号，那肯定就冲突了。

​	每提交一个新版本，实际上Git就会把他们自动串成一条时间线。

#### 5.2、版本回退

​	首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。 

​	现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`，就可以使用`git reset`命令 

```
$ git reset --hard HEAD^
HEAD is now at dc9fea2 add distributed
```

​	只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个`append GPL`的`commit id`是`1094adb...`，于是就可以指定回到未来的某个版本：

```
$ git reset --hard 1094a
HEAD is now at 83b0afe append GPL
```

* Git提供了一个命令git reflog用来记录你的每一次命令

#### 5.3、小结

* HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id.
* 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
* 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

## 6、工作区和暂存区

#### 6.1、概念

工作区（Working Directory）就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区。

版本库（Repository），Git的版本库里存了很多东西，其中最重要的就是成为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

* `git add` 把文件添加进去，实际上就是把文件修改添加到暂存区；
* `git commit` 提交更改，实际上就是把暂存区的所有内容提交到当前分支。

#### 6.2、小结

​	暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。

## 7、管理修改

每次修改，如果不用git add到暂存区，那就不会加入到commit中。

## 8、撤销修改

#### 8.1、`git checkout -- file` 可以丢弃工作区的修改：

```
＄git checkout -- readme.txt
```

命令 git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

* 一种是readme.txt自修改之后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
* 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

#### 8.2 、`git reset HEAD<file>` 可以把暂存区的修改撤销掉（unstage），重新放回工作区

```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt
```

#### 8.3、小结

* 场景1：当你乱改了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file` 。
* 场景2：当你不但乱改了工作区某个文件的内容，还添加到了暂存区，想丢弃修改，分两步，第一步用命令`git reset HEAD<file>` ,就回到了场景1，第二步按场景1操作。
* 场景3：已经提交了不合适的修改到版本库，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。 

## 9、删除文件

#### 9.1、`rm` 命令

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用`rm` 命令删除：

```
$ rm test.txt
```

这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致，`git status` 命令会立刻告诉你哪些文件被删除了：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm` 删除，并且`git commit` :

```
$ git rm test.txt
rm 'test.txt'

$ git commit -m"remove test.txt"
[master 43c5cb1] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```

现在，文件就从版本库中被删除了。

另一种情况是删错了，因为版本库还有呢，所以可以很轻松地把误删除的文件恢复到最新版本：

```
$ git checkout -- test.txt
```

`git checkout` 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

#### 9.2、小结

* 命令`git rm` 用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

## 10、远程仓库

#### 10.1、简介

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。 找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

[GitHub](https://github.com/)的神奇的网站 。 

#### 10.2、创建SSH密钥和公钥

在继续阅读后续内容前，请自行注册GitHub帐号。由于你的本地IGit仓库和Github仓库之间的传输是通过SSH加密的，所以，需要一点设置：

**第1步：**创建SSH key。在用户主目录下，看看有没有shh目录，如果有，在看看这个目录下有没有`id_rsa`和 `id_isa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

* 注意：如果在ssh后面加上空格，会得到Bad escape character 'ygen'的错误。

你需要把邮件地址换成你自己的又邮件地址，然后一路回车，使用默认值即可，由于这个Key也不少用于军事目的，所以要无需设置设置密码。

如果一切顺利的话，可以在用户主目录找到`.ssh` 目录，里面有`id_rssa` 和`id_rsa.pub` 两个文件，这两个就是SSH Key的密钥对，`id_rsa` 是私钥，不能泄露出去，`id_rsa.pub` 是公钥，可以放心地告诉任何人。

**第2步：**登录GitHub，打开"Account setting"，“SSH Keys”的页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框李粘贴`id_rsa.pub` 文件的内容：

点“Add Key”，你就应该看到已经添加的Key 

​	为什么GitHub需要SSH Key?因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

​	当然，GitHub允许你添加多个Key。假定你又若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送。

​	最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能该）。所以，不要把敏感信息放进去。

​	如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所有别人也是看不见。这个方法我们后面会讲到的，相当简单，公司内部开发必备。

确保你拥有一个GitHub帐号后，我们就开始远程仓库的学习。

## 11、添加远程库

1. 首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库： 

2. 在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库： 

3. 现在，我们根据GitHub的提示，在本地的`learngit`仓库下运行命令：

   ```
   $ git remote add origin git@github.com:michaelliao/learngit.git
   ```

   请千万注意，把上面的`michaelliao`替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

   添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

```
     $ git push -u origin master
     Counting objects: 13, done.
     Delta compression using up to 4 threads.
     Compressing objects: 100% (9/9), done.
     Writing objects: 100% (13/13), 1.09 KiB | 186.00 KiB/s, done.
     Total 13 (delta 2), reused 0 (delta 0)
     remote: Resolving deltas: 100% (2/2), done.
     To github.com:Rzihan/learngit.git
     
     - [new branch]      master -> master
       Branch 'master' set up to track remote branch 'master' from 'origin'.
```

​        把本地库的内容推送到远程，用`git push` 命令，实际上是把当前分支`master` 推送到远程。

​	由于远程库是空的，我们第一次推送`master` 分支时，加上了`-u` 参数，Git不但会把本地的`master` 分支内容推送到远程新道德`master` 分支，还会吧本地的`master` 分支和远程的`master` 分支关联起来，在以后的推送或者拉取就可以简化命令。

​	推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样；

​	从现在起，只要本地作了提交，就可以通过命令：

```
$ git push origin master
```

​	把本地	`master` 分支的罪行修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

#### 11.1、SSH警告

​	当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (13.250.177.223)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
```

​	这个因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

​	Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
Warning: Permanently added 'github.com,13.250.177.223' (RSA) to the list of known hosts.
```

​	这个警告只会出现一次，后面的操作就不会有任何警告了。

​	如果你实在担心有人貌丑GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

#### 11.2、小结

* 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`;
* 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
* 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master` 推送最新修改；
* 分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，在把本地提交推送一下就完成了同步。

## 12、从远程库克隆

上次我们讲了先有本地库，后有远程库的时候，如何关联远程库。

现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

首先，登录GitHub，创建一个新的仓库，名字叫`gitskills`:

我们勾选`Initialize this repository with a README`,这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到`README.md` 文件：

#### 12.1、使用命令`git clone` 克隆一个本地库：

```
$ git clone git@github.com:Rzihan/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

注意吧Git库的地址换成你自己的，然后进入`gitskills`目录看看，已经有`README.md`文件了:

如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。

你也许还注意到，GitHub给出的地址不止一个，还可以用`http://github.com/Rzihan/gitskills.git` 这样的地址。实际上，Git支持多种协议，默认的`git：//`使用ssh，但也可以使用`https`等其他协议。

使用`http`处理速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`.

#### 12.2、小结

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone` 命令克隆。

Git支持多种协议，包括`https`，但通过`ssh` 支持的原生`git` 协议速度最快。

## 13、分支管理

分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完在一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，知道开发完毕后，在一次性合并到原来的分支上，这样，既安全有不影响别人工作。

其他版本控制系统如SVN等都有分支管理，但是用过之后你会发现，这些版本控制系统创建和切换分支比蜗牛还慢，简直让人无法忍受，结果分支功能成了摆设，大家都不去用。

但Git的分支是与众不同的，无论创建，切换和删除分支，Git在1秒钟之内就能完成！无论你的版本库是1个文件还是1万个文件。

## 14、创建与合并分支

1. 首先，我们创建`dev`分支，然后切换到`dev`分支

```
$ git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout`命令加上`-b` 参数表示创建并切换，相当与以下两条命令

```
$ git branch dev

$ git checkout dev

Switch to branch 'dev'
```

然后，用`git branch` 命令查看当前分支：

```
$ git branch

* dev
  master
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

然后，我们就可以在`dev`分支上正常提交，比如对readme.txt做个修改，加上一行：

```
Creating a new branch is quick.
```

然后提交：

```
$ git add README.md
$ git commit -m "branch README.md"
[dev 2a78c99] branch README.md
 1 file changed, 2 insertions(+), 1 deletion(-)
```

现在，`dev`分支的工作完成，我们就可以切换会`master`分支；

```
$ git checkout master
Switched to branch 'master'
```

切换会`master`分支后，在查看一个README.md文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master` 分支此刻的提交点并没有变；

现在，我们把`dev`分支的工作成果合并到`master`分支上

```
$ git merge dev
Updating 6bd0cf1..2a78c99
Fast-forward
 README.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

`git merge` 命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和`dev`分支的最新提交是完全一样的。

注意到上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。

当然，也不是每次合并都能`Fast-forward`，我们后面会讲其他方式的合并。

合并完成后，就可以放心地删除`dev`分支了：

```
$ git branch -d dev
Deleted branch dev (was 2a78c99).
```

因为创建、合并和删除分支非常快，所以Git鼓励你是用分支完成某个任务，合并后再删掉分支，这和直接在`master` 分支上工作效果是一样的，但过程更安全。

#### 14.1、小结

Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name> 

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

## 15、解决冲突

​	当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。用`git log  --graph` 

## 16、分支管理策略

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

下面我们实战一下`--no-ff`方式的`git merge`：

首先，仍然创建并切换`dev`分支：

```
$ git checkout -b dev

Switched to a new branch 'dev'
```

修改readme.txt文件，并提交一个新的commit；

```
$ git add readme.txt

$ git commit -m "add merge"

[dev f52c633] add merge

 1 file changed,1 insertion(+)
```

现在，我们切换回`master`：

```
$ git checkout master
Switched to branch 'master'
```

准备合并`dev`分支，请注意`--no-ff`参数，表示禁用`Fast forward`：

```
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

因为本次合并要创建一个新的commit，所以加上`-m`参数，把commit描述写进去。

合并后，我们用`git log`看看分支历史：

```
$ git log --graph --pretty=oneline --abbrev-commit
*   e1e9c68 (HEAD -> master) merge with no-ff
|\  
| * f52c633 (dev) add merge
|/  
*   cf810e4 conflict fixed
...
```

### 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

### 小结

Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并

## 17、bug分支

软件开发中，bug就像是家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支`issue-101`来修复它，但是，等等，当前正在`dev`进行的工作还没有提交，并不是你不想提交，而是工作只进行到一般，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该BUG，怎么办？

幸好，Git还提供了一个stash功能，可以把当前工作现场“储存”起来，等以后恢复现场后继续工作；

```
$ git stash
Saved working directory and index state WIP on dev: f4b3e54 merge with no-ff
```

现在，用`git status`查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。

首先确定要在哪个分支上修复bug，假定需要在`master`分支上修复，就从`master`创建临时分支：

```
 $ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

$ git checkout -b issue-101
Switched to a new branch 'issue-101'
```

修复完成后，切换到master分支，并完成合并，最后删除issue-101.

```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

$ git merge --no-ff -m "merged bug fix 101" issue-101
Merge made by the 'recursive' strategy.
 README.md | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
```

工作区是干净的，刚才的工作现场存到哪去了？用`git stash list`命令看看： 

```
$ git stash list
stash@{0}: WIP on dev: f52c633 add merge
```

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；

另一种方式是用`git stash pop`，恢复的同时把stash内容也删了：

```
$ git stash pop
On branch dev
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   hello.py

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

Dropped refs/stash@{0} (5d677e2ee266f39ea296182fb2354265b91b3b2a)
```

再用`git stash list`查看，就看不到任何stash内容了：

```
$ git stash list
```

你可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令：

```
$ git stash apply stash@{0}
```

#### 小结

* 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
* 当手头工作没有完成时，先把工作现场`git stash` 一下，然后去 修复bug，修复后，在`git stash pop` ，回到工作现场。
* 开发一个新feature，最好新建一个分支；
* 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name> `强行删除。

## 18、多人协作

当你从远程仓库克隆时，实际上Git自动把本地的`master` 分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`，要查看远程库的信息，用`git remote`

```
$ git remote

origin
```

或者，用`git remote -v`显示更详细的信息：

```
$ git remote -v
origin  git@github.com:Rzihan/gitskills.git (fetch)
origin  git@github.com:Rzihan/gitskills.git (push)
```

上面显示了可以抓取和推送的`origin`的地址。如果没有推送权限，就看不到push的地址。

##### 推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地本质，这样。Git就会把该分支推送到远程库对应的分支上；

```
$git push origin master
```

如果要推送其他分支，比如`dev`，就改成：

```
$ git push origin dev
```

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？ 

* `master`分支是主分支，因此要时刻与远程同步;
* `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
* bug分支只用于在本地修复bug，就没必要推送到远程了，除非老板要看看你每周到底修复了几个bug；
* feature分支是否推送到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定。

##### 抓取分支

多人协作时，大家都会往`master`和`dev`分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆。

```
$ git clone git@github.com:michaelliao/learngit.git
Cloning into 'learngit'...
remote: Counting objects: 40, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 40 (delta 14), reused 40 (delta 14), pack-reused 0
Receiving objects: 100% (40/40), done.
Resolving deltas: 100% (14/14), done.
```

当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的`master`分支，不信可以用`git branch`命令看看；

```
$ git branch
* master
```

现在，你的小伙伴要在`dev`分支上开发，就必须创建远程的`origin`的`dev`分支到本地，于是他用这个命令创建本地`dev`分支

```
$ git checkout -b dev origin/dev
```

现在，他就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程：

```
$ git add env.txt

$ git commit -m "add env"
[dev 7a5e5dd] add env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   f52c633..7a5e5dd  dev -> dev
```

你的小伙伴已经向`origin/dev`分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：

```
$ cat env.txt
env

$ git add env.txt

$ git commit -m "add new env"
[dev 7bd91f1] add new env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt

$ git push origin dev
To github.com:michaelliao/learngit.git
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，解决冲突，再推送： 

```
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

`git pull`也失败了，原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接：

```
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
```

再pull：

```
$ git pull
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
```

这回`git pull`成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的[解决冲突](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840202368c74be33fbd884e71b570f2cc3c0d1dcf000)完全一样。解决后，提交，再push：

```
$ git commit -m "fix env conflict"
[dev 57c53ab] fix env conflict

$ git push origin dev
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   7a5e5dd..57c53ab  dev -> dev
```

因此，多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示 `no tracking information`，则说明本地分支和远程分支的连接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

##### 小结

* 查看远程库信息，使用`git remote -v`;
* 本地新建的分支如果不推送到远程，对其他人就是不可见；
* 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`驻区远程的新提交
* 在本地创建和远程分支对应的分支，使用`git checkou -b branch-name origin/branch-name`,本地和远程分支的名称最好一致。
* 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`;
* 从远程抓取分支，使用`git pull`,如果有冲突，要先处理冲突。

## 19、Rebase

$git rebase

rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了

#### 小结

* rebase操作可以把本地未push的分叉提交历史整理成直线；
* rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

## 20、标签管理

#### 20.1、概念

标签（tag）就是一个让人容易记住的有意义的名字，它跟某个人commit绑在一起

#### 20.2、创建标签

* 切换到需要打标签的分支上，敲命令`git tag <name>`就可以打一个新标签  

```
$ git tag v1.0
```

* 可以用命令`git tag`查看所有标签：

```
$ git tag
```

* 查看历史提交的版本号

```
$ git log --pretty=oneline --abbrev-commit
```

* 查看标签的详细信息

```
git show<tagname>
```

* 创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字 

```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

##### 小结：

* 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
* 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
* 命令`git tag`可以查看所有标签。

#### 20.3、操作标签

```
$ git tag -d v0.1 删除标签
$ git push origin <tagname> 推送某个标签到远程
$ git push origin --tags 一次性推送尚未推送到远程的本地标签
$ git tag -d <tagename> 可以删除一个本地标签
$ git push origin :refs/tags/<tagname> 可以删除一个远程标签
```

## 21、自定义

#### 21.1、忽略特殊文件

有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，每次`git status`都会显示`Untracked files ...`，有强迫症的童鞋心里肯定不爽。

好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的`.gitignore`文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写`.gitignore`文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：<https://github.com/github/gitignore>

忽略文件的原则是：

1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的`.class`文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

举个例子：

假设你在Windows下进行Python开发，Windows会自动在有图片的目录下生成隐藏的缩略图文件，如果有自定义目录，目录下就会有`Desktop.ini`文件，因此你需要忽略Windows自动生成的垃圾文件：

```
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini
```

然后，继续忽略Python编译产生的`.pyc`、`.pyo`、`dist`等文件或目录：

```
# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build
```

加上你自己定义的文件，最终得到一个完整的`.gitignore`文件，内容如下：

```
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build

# My configurations:
db.ini
deploy_key_rsa
```

最后一步就是把`.gitignore`也提交到Git，就完成了！当然检验`.gitignore`的标准是`git status`命令是不是说`working directory clean`。

使用Windows的童鞋注意了，如果你在资源管理器里新建一个`.gitignore`文件，它会非常弱智地提示你必须输入文件名，但是在文本编辑器里“保存”或者“另存为”就可以把文件保存为`.gitignore`了。

有些时候，你想添加一个文件到Git，但发现添加不了，原因是这个文件被`.gitignore`忽略了：

```
$ git add App.class
The following paths are ignored by one of your .gitignore files:
App.class
Use -f if you really want to add them.
```

如果你确实想添加该文件，可以用`-f`强制添加到Git：

```
$ git add -f App.class
```

或者你发现，可能是`.gitignore`写得有问题，需要找出来到底哪个规则写错了，可以用`git check-ignore`命令检查：

```
$ git check-ignore -v App.class
.gitignore:3:*.class    App.class
```

Git会告诉我们，`.gitignore`的第3行规则忽略了该文件，于是我们就可以知道应该修订哪个规则。

##### 小结

- 忽略某些文件时，需要编写`.gitignore`；
- `.gitignore`文件本身要放到版本库里，并且可以对`.gitignore`做版本管理！

#### 21.2、配置别名

有没有经常敲错命令？比如`git status`？`status`这个单词真心不好记。

如果敲`git st`就表示`git status`那就简单多了，当然这种偷懒的办法我们是极力赞成的。

我们只需要敲一行命令，告诉Git，以后`st`就表示`status`：

```
$ git config --global alias.st status
```

好了，现在敲`git st`看看效果。

当然还有别的命令可以简写，很多人都用`co`表示`checkout`，`ci`表示`commit`，`br`表示`branch`：

```
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
```

以后提交就可以简写成：

```
$ git ci -m "bala bala bala..."
```

`--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

在[撤销修改](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374831943254ee90db11b13d4ba9a73b9047f4fb968d000)一节中，我们知道，命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个`unstage`别名：

```
$ git config --global alias.unstage 'reset HEAD'
```

当你敲入命令：

```
$ git unstage test.py
```

实际上Git执行的是：

```
$ git reset HEAD test.py
```

配置一个`git last`，让其显示最后一次提交信息：

```
$ git config --global alias.last 'log -1'
```

这样，用`git last`就能显示最近一次的提交：

```
$ git last
commit adca45d317e6d8a4b23f9811c3d7b7f0f180bfe2
Merge: bd6ae48 291bea8
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 22:49:22 2013 +0800

    merge & fix hello.py
```

甚至还有人丧心病狂地把`lg`配置成了：

```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

来看看`git lg`的效果：

![git-lg](https://cdn.liaoxuefeng.com/cdn/files/attachments/00138492662982594cbd1a942114472aeeb5f0a502faed1000/0)

为什么不早点告诉我？别激动，咱不是为了多记几个英文单词嘛！

##### 配置文件

配置Git的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在`.git/config`文件中：

```
$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```

别名就在`[alias]`后面，要删除别名，直接把对应的行删掉即可。

而当前用户的Git配置文件放在用户主目录下的一个隐藏文件`.gitconfig`中：

```
$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
```

配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

##### 小结

给Git配置好别名，就可以输入命令时偷个懒。我们鼓励偷懒。

#### 21.3、搭建Git服务器

##### 搭建Git服务器

在[远程仓库](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)一节中，我们讲了远程仓库实际上和本地仓库没啥不同，纯粹为了7x24小时开机并交换大家的修改。

GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。

搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的`apt`命令就可以完成安装。

假设你已经有`sudo`权限的用户账号，下面，正式开始安装。

第一步，安装`git`：

```
$ sudo apt-get install git
```

第二步，创建一个`git`用户，用来运行`git`服务：

```
$ sudo adduser git
```

第三步，创建证书登录：

收集所有需要登录的用户的公钥，就是他们自己的`id_rsa.pub`文件，把所有公钥导入到`/home/git/.ssh/authorized_keys`文件里，一行一个。

第四步，初始化Git仓库：

先选定一个目录作为Git仓库，假定是`/srv/sample.git`，在`/srv`目录下输入命令：

```
$ sudo git init --bare sample.git
```

Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以`.git`结尾。然后，把owner改为`git`：

```
$ sudo chown -R git:git sample.git
```

第五步，禁用shell登录：

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑`/etc/passwd`文件完成。找到类似下面的一行：

```
git:x:1001:1001:,,,:/home/git:/bin/bash
```

改为：

```
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

这样，`git`用户可以正常通过ssh使用git，但无法登录shell，因为我们为`git`用户指定的`git-shell`每次一登录就自动退出。

第六步，克隆远程仓库：

现在，可以通过`git clone`命令克隆远程仓库了，在各自的电脑上运行：

```
$ git clone git@server:/srv/sample.git
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.
```

剩下的推送就简单了。

##### 管理公钥

如果团队很小，把每个人的公钥收集起来放到服务器的`/home/git/.ssh/authorized_keys`文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用[Gitosis](https://github.com/res0nat0r/gitosis)来管理公钥。

这里我们不介绍怎么玩[Gitosis](https://github.com/res0nat0r/gitosis)了，几百号人的团队基本都在500强了，相信找个高水平的Linux管理员问题不大。

##### 管理权限

有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。[Gitolite](https://github.com/sitaramc/gitolite)就是这个工具。

这里我们也不介绍[Gitolite](https://github.com/sitaramc/gitolite)了，不要把有限的生命浪费到权限斗争中。

##### 小结

- 搭建Git服务器非常简单，通常10分钟即可完成；
- 要方便管理公钥，用[Gitosis](https://github.com/sitaramc/gitolite)；
- 要像SVN那样变态地控制权限，用[Gitolite](https://github.com/sitaramc/gitolite)。