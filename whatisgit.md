

# #1 啥是Git

---

> 本文档为本人阅读[教程](https://www.liaoxuefeng.com/wiki/896043488029600)的学习笔记或者部分摘录

## 一. Git简介

### 1. Git的诞生

- Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件。
- 在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码。
- 到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理。
- Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git。一个月之内，Linux系统的源码已经由Git管理了。
- Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

### 2. 集中式与分布式的区别

- 集中式版本控制系统
  - 版本库集中存放在中央服务器，干活需先从中央服务器取得最新版本，完成之后再推送至中央服务器。好比需要从图书馆中修改一本书。
  - 需要联网工作，可能遇到网速慢从而导致提交速度慢的情况。
- 分布式版本控制系统
  - 没有“中央服务器”，每个人电脑上存在完整的版本库，因此不需要联网运作，多人协作时仅需把自己的修改推送给对方即可。
  - 通常情况下，会有一台充当“中央服务器”的电脑，但作用仅仅是方便“交换”大家的修改。

---

## 二.安装Git

> 本人使用的是 WSL Ubuntu 22.04

### 1. 判断是否安装Git

- 在终端中输入`git`。
- 若显示没有安装，则输入`sudo apt-get install git`，等待即可完成Git的安装。

### 2. 版本库

- 什么是版本库

  - 版本库又名仓库，可以理解为一个目录，这个目录的所有文件都可以被Git管理起来。
  - 目录里的所有文件的修改或删除，Git都能跟踪，以便追踪历史或还原文件。

- 创建版本库

  - 选择一个合适的地方，创建一个空目录。

    ~~~
    $ mkdir repo
    $ cd repo
    $ pwd
    /home/liquan/repo
    ~~~

    > mkdir命令用于创建一个目录，cd命令用于显示当前目录的名称或切换目录位置，pwd用于显示当前目录

  - 通过`git init`命令把这个目录变成Git可以管理的仓库。

    ~~~
    $ git init
    Initialized empty Git repository in /home/liquan/repo/.git/
    ~~~

    此时Git就把仓库建好了，注意不要手动修改新产生的目录`.git`中的文件。

### 3. 添加文件到版本库

- 一些需注意的点

  - 所有版本控制系统只能跟踪文本文件的改动。

  - 不建议使用Windows自带的记事本来编辑文本文件，推荐使用强大且免费的*Visual Studio Code*。

- 添加文件

  - 编写一个文本文档`readme.txt`：

    ~~~
    Git is a vesion control system.
    Git is a free software.
    ~~~

  - 将该文件放到`repo`目录（或子目录）下。

  - 用命令`git add`告诉Git把文件添加到仓库

    ~~~
    $ git add readme.txt
    ~~~

  - 用命令`git commit`告诉Git把文件提交到仓库

    ~~~
    $ git commit -m "wrote a readme file"
    ~~~
    
    > `-m`后输入本次提交的说明；`1 file changed`表示一个文件被改动；`2 insertions`表示插入了2行内容

---

## 三.版本控制

### 1. 文件修改跟踪

- 对`readme.txt`的跟踪

  - 将`readme.txt`的内容改成以下内容：

    ~~~ 
    Git is a distributed version control system.
    Git is a free software.
    ~~~

  - 运行`git status`命令查询结果

    ~~~
    $ git status
    ~~~

    > `git status`命令可以让我们时刻掌握仓库当前的状态

  - 运行`git diff`查看具体修改的内容

    ~~~
    $ git diff readme.txt
    ~~~

- 提交对`readme.txt`的修改

  - 与提交新文件的两步相同，首先`git add`

    ~~~
    $ git add readme.txt
    ~~~

  - 执行第二步`git commit`前，再运行`git status`看看当前仓库的状态

    ~~~
    $ git status
    ~~~

    执行结果告诉我们，将要被提交的修改包括`readme.txt`，下一步即可放心提交

  - 提交修改

    ~~~
    $ git commit -m "add distributed"
    ~~~

    提交后再运行`git status`查看仓库当前状态

    ~~~
    $ git status
    ~~~

    Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。

### 2. 版本回退

- 再对`readme.txt`进行第二次修改，产生第三个版本

  - 内容修改为：

    ~~~
    Git is a distributed version control system.
    Git is a free software distributed under the GPL.
    ~~~

  - 提交第二次修改

    ~~~
    $ git add readme.txt
    $ git status
    $ git commit -m "append GPL"
    $ git status
    ~~~

- 查看历史记录

  - 用`git log`查看历史记录

    ~~~
    $ git log
    ~~~

    `git log`命令显示从最近到最远的提交日志，我们可以看到3次提交。其中`commit`后一长串字符为`commit id`（版本号）。

  - 简化历史信息

    若想简化生成的日志，可加上`--pretty=oneline`参数

    ~~~
    $ git log --pretty=oneline
    ~~~

- 回退至上一版本

  - 在Git中，用`HEAD`表示当前版本，上一个版本表示为`HEAD^`,上上版本为`HEAD^^`,上N个版本可写为`HEAD~N`。

  - 将当前版本`append GPL`回退至上一版本`add distributed`，可用`git reset`命令

    ~~~
    $ git reset --hard HEAD^
    ~~~

  - 查看`readme.txt`，发现果然被回退了一个版本。此时再用`git log`查看历史记录，可发现第三个版本`append GPL`不见了，在命令行窗口关闭之前，可通过版本号`commit id`回到指定未来版本。

- 还原至未来版本

  - 依然使用`git reset`命令

    ~~~
    $ git reset --hard 589bc
    ~~~

    其中`589bc`为版本号前几位，Git在进行还原时会自动进行寻找。

  - 若没有`commit id`（版本号），则可通过Git的命令`git reflog`来记录每一次命令

    ~~~
    $ git reflog
    ~~~

    从输出结果可知，`append GPL`的`commit id`是`589bc74`。通过此方式可提供未来版本的版本号从而回到未来版本。

### 3. 工作区和暂存区

- 工作区
  - 工作区就是电脑里能看到的目录，例如上面创建的`repo`文件夹就是一个工作区。
- 隐藏目录`.git`
  - 工作区中有一个隐藏目录`.git`，这个不是工作区，而是Git的版本库。
  - Git的版本库中存有许多东西，其中最重要的就是称为stage（或index）的暂存区，还有Git为我们创建的第一个分支`master`，以及指向`master`的一个指针`HEAD`。
- 添加文件到版本库的过程
  - 第一步用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区。
  - 第二步用`git commit`提交修改，实际上就是把暂存区的所有内容提交到当前分支。

### 4. 管理修改

- Git管理修改而非文件

  - 对`readme.txt`增加一个修改，如添加一行内容

    ~~~
    Git tracks changes.
    ~~~

  - 使用`cat`命令，显示文档中的所有内容

    ~~~
    $ cat readme.txt
    Git is a distributed version control system.
    Git is a free software distributed under GPL.
    Git tracks changes.
    ~~~

  - 随后添加文件

    ~~~
    $ git add readme.txt
    $ git status
    ~~~

  - 再次对`readme.txt`进行修改，并使用`git cat`进行查看

    ~~~
    $ cat readme.txt
    Git is a distributed version control system.
    Git is a free software distributed under GPL.
    Git tracks changes of files.
    ~~~

  - 提交文件并查看仓库状态

    ~~~
    $ git commit -m "git tracks changes"
    $ git status
    ~~~

    运行结果可知，第二次修改没有被提交。

  - 结论

    - 上面使用`git add`后，只把工作区的第一次修改放入暂存区准备提交，第二次修改没有被放入暂存区。
    - `git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

  - 查看工作区和版本库中最新版本的区别

    ~~~
    $ git diff HEAD -- readme.txt
    ~~~

    可见第二次修改确实没有被提交。

### 5.撤销修改

- 丢弃工作区的修改

  - 假设你在`readme.txt`中不小心多写了一行无用的内容：

    ~~~
    Git is a distributed version control system.
    Git is a free software distributed under GPL.
    Git tracks changes of files.
    My stupid boss still prefers SVN.
    ~~~

    及时发现错误后，可以直接手动在`readme.txt`中将多余的内容删除。

  - 还可以利用命令`git checkout -- file`丢弃工作区中的修改

    ~~~
    $ git checkout -- readme.txt
    ~~~

    上述命令会将`readme.txt`在工作区中的修改全部撤销，这里有两种情况：

    - 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态。
    - 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

- 丢弃已添加到到暂存区的修改

  - 假设你已将有错误内容的`readme.txt`通过`git add`添加到暂存区：

    ~~~
    $ git add readme.txt
    ~~~

    用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉，重新放回工作区

    ~~~
    $ git reset HEAD readme.txt
    ~~~

    重新放回工作区后，使用命令`git checkout -- file`即可丢弃在工作区的修改。

### 6. 删除文件

- 删除工作区中已提交至版本库的文件

  - 假定我们添加了一个新文件`test.txt`到Git并且提交

    ~~~
    $ git add test.txt
    $ git commit -m "add test.txt"
    ~~~

    此时我们可以使用命令`rm`将该文件删除

    ~~~
    $ rm test.txt
    ~~~

    此时就将工作区中的`test.txt`删除了，若使用`git status`

    ~~~
    $ git status
    ~~~

    运行结果会告诉我们哪些文件被删除了。

- 对版本库的处理

  - 若我们确实要从版本库中删除该文件，则使用命令`git rm`删掉，并`git commit`

    ~~~
    $ git rm test.txt
    $ git commit -m "remove test.txt"
    ~~~

    此时文件就已从版本库中删除。

  - 若我们错删文件，则可通过`git checkout`命令将误删的文件恢复到最新版本

    ~~~
    $ git checkout -- test.txt
    ~~~

    `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

    从来没有被添加到版本库就被删除的文件，是无法恢复的。

---

## 四. 远程仓库

### 1. Github

- 创建SSH Key

  - 由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，故需要进行一些设置。

  - 打开Shell（Windows下为Git Bash），创建SSH Key：

    ~~~
    $ ssh-keygen -t rsa -C "646287195@qq.com"
    ~~~

    随后一路回车使用默认值。完成后可在用户主目录里找到`.ssh`目录，里面有`id_rsa`、`id_rsa.pub`两个文件，即SSH Key的密钥对。

- 在Github中添加Key

  - 登陆GitHub，打开“Account settings”，“SSH Keys”页面。
  - 点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`的内容。
  - 点“Add Key”，就可以看到已经添加的Key。

- 添加远程库

  - 在Github建立一个Git仓库，点击右上角“+”展开中的“New repository"。
  - 填好Repository Name，其他保持默认值后点击Create repository。

- 将新的Github仓库与本地仓库进行关联

  - 在本地的`repo`仓库下运行命令：

    ~~~
    $ git remote add origin git@gitgub.com:lq-quan/learngit.git
    ~~~

    添加后，远程库的名字就叫`origin`，这是Git默认的叫法。

  - 将本地库的所有内容推送到远程库上

    ~~~
    $ git push -u origin master
    ~~~

    把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

    第一次推送`master`分支时，加上了`-u`参数，此后只要本地作了提交，就可以通过以下命令

    ~~~
    $ git push origin master
    ~~~

    把本地`master`分支的最新修改推送至GitHub。

- 删除远程库

  - 查看远程库信息，使用命令：

    ~~~
    $ git remote -v
    ~~~

  - 根据远程库的名字进行删除，如删除`origin`：

    ~~~
    $ git remote rm origin
    ~~~

    此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。

### 2. 从远程库克隆

- 创建一个新远程库

  - 登录Github，创建一个新的仓库，名为`gitskills`。

  - 创建时勾选`Initialize this repository with a README`，创建完毕后可以看到`README.md`文件。

  - 用命令`git clone`克隆一个本地库

    ~~~
    $ git clone git@github.com:lq-quan/gitskills.git
    ~~~

  - 进入`gitskills`目录查看，可以看到有`README.md`文件了

    ~~~
    $ cd gitskills
    $ ls
    README.md
    ~~~

---

## 五.分支管理

### 1. 创建与合并分支

- 什么是分支
  - 每次文件提交，Git都把它们串成一条时间线，这条时间线就是一个分支。
  - 截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。
  - `HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

- 创建分支

  - 创建一个`dev`分支，然后切换到`dev`分支

    ~~~
    $ git checkout -b dev
    ~~~

    `git checkout`命令加上`-b`参数，表示创建并切换，相当于：

    ~~~
    $ git branch dev
    $ git checkout dev
    ~~~

- 查看分支

  - 用`git branch`命令查看当前分支：

    ~~~
    $ git branch
    * dev
      master
    ~~~

    `git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

  - 在`dev`分支上正常提交，如对`readme.txt`作一个修改，加上一行：

    ~~~
    Creating a new branch is quick.
    ~~~

    然后提交

    ~~~
    $ git add readme.txt
    $ git commit -m "branch test"
    ~~~

  - 切换回`master`分支

    ~~~
    $ git checkout master
    ~~~

    切换回`master`分支后，再查看`readme.txt`，发现刚刚添加的内容不见了，现在我们需要把`dev`分支的工作成果合并到分支`master`上

    ~~~
    $ git merge dev
    ~~~

    执行结果中`Fast forward`告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交。

- 删除分支

  - 合并完成后，就可以删除`dev`分支了

    ~~~
    $ git branch -d dev
    ~~~

  - 查看`branch`

    ~~~
    $ git branch
    ~~~

    可发现只剩下了`master`分支。

- 一个更容易理解的创建与切换分支命令

  - 切换分支`git checkout <branch>`与前面的撤销修改`git checkout -- <file>`易混淆。

  - Git提供了更科学的`git switch`命令来切换分支：

    创建并切换到新的`dev`分支：

    ~~~
    $ git switch -c dev
    ~~~

    直接切换到已有的`master`分支：

    ~~~
    $ git switch master
    ~~~

    > Git鼓励我们大量使用分支。

### 2. 合并冲突与解决

- 为演示解决冲突，我们创建并使用新分支`feature1`

- 准备新的`feature1`分支

  - 使用更为科学的分支创建与切换命令

    ~~~
    $ git switch -c feature1
    ~~~

  - 修改`readme.txt`，使最后一行改为：

    ~~~
    Creating a new branch is quick and simple.
    ~~~

  - 在`feature1`分支上提交

    ~~~
    $ git add readme.txt
    $ git commit -m "and simple"
    ~~~

- 回到`master`分支

  - 切换回`master`分支

    ~~~
    $ git switch master
    ~~~

  - 在`master`分支上把最后一行改为：

    ~~~
    Creating a new branch is quick & simple.
    ~~~

  - 提交

    ~~~
    $ git add readme.txt
    $ git commit -m "& simple"
    ~~~

- 出现冲突

  - 我们尝试将两个分支合并

    ~~~
    $ git merge feature1
    ~~~

    Git会告诉我们，`readme.txt`文件存在冲突，必须手动解决冲突后再提交。

  - 可使用`git status`命令查看冲突的文件

    ~~~
    $ git status
    ~~~

    若此时我们查看`readme.txt`，发现Git标记出了不同分支的内容。

  - 我们修改如下后保存

    ~~~
    Creating a new branch is quick and simple.
    ~~~

    再提交

    ~~~
    $ git add readme.txt
    $ git commit -m "conflict fixed"
    ~~~

  - 可使用带参数的`git log`查看分支的合并情况

    ~~~
    $ git log --graph --pretty=oneline --abbrev-commit
    ~~~

  - 需要注意的是，合并操作只对对当前所在分支产生影响；无论是否存在冲突，合并之后，`feature1`分支都不会发生变化。

  - 最后，删除`feature1`分支

    ~~~
    $ git branch -d feature1
    ~~~

### 3. 分支管理策略

- 禁用`fast forward`模式

  - 在`fast forward`分支合并模式下，删除分支后会丢掉分支信息

    强制禁用`fast forward`模式，Git就会在merge时生成一个新的commit

    下面使用`--no-ff`方式的`git merge`。

  - 首先创建并切换`dev`分支

    ~~~
    $ git switch -c dev
    ~~~

    修改`readme.txt`，如添加一行：

    ~~~
    We have to merge the branch.
    ~~~

    提交修改：

    ~~~
    $ git add readme.txt
    $ git commit -m "add merge"
    ~~~

  - 准备合并，切换回`master`分支

    ~~~
    $ git switch master
    ~~~

  - 开始合并`dev`分支，注意`--no-ff`参数

    ~~~
    $ git merge --no-ff -m "merge with no-ff" dev
    ~~~

    由于本次合并要创建一个新的commit，所以加上`-m`参数，把commit描述写进去。

  - 合并后，使用`git log`查看分支历史

    ~~~
    $ git log graph --pretty=oneline --abbrev-commit
    ~~~

- 分支策略

  - 首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活。
  - 干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本。
  - 每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

### 4. Bug分支

- 工作区的“储藏”与恢复

  - Git提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

    例如现在正在分支`dev`上进行工作，突然收到任务要紧急修复`master`上的Bug，则使用下面命令存储工作现场：

    ~~~
    $ git stash
    ~~~

    现在，用`git status`查看工作区，就是干净的（除非有没有被Git管理的文件）。

  - 首先确定要在哪个分支上修复bug，假定需要在`master`分支上修复，就从`master`创建临时分支

    ~~~
    $ git checkout master
    $ git checkout -b issue-101
    ~~~

  - 修复Bug，然后提交：

    ~~~
    $ git add readme.txt
    $ git commit -m "fix bug 101"
    ~~~

  - 修复完成，切换回`master`分支，并完成合并，最后删除`issue-101`分支

    ~~~
    $ git switch master
    $ git merge --no-ff -m "merged bug fix 101" issue-101
    ~~~

  - 回到`dev`继续工作

    ~~~
    $ git switch dev
    $ git status
    ~~~

    用命令`git stash list`查看保存的工作现场

    ~~~
    $ git stash list
    ~~~

    使用`git stash apply`来恢复，但仍需命令`git stash drop`来删除`stash`的内容

    也可直接使用命令`git stash pop`，恢复的同时把stash内容也删除了。

  - 多次`stash`

    先使用`git stash list`查看，然后选择恢复指定的stash

    ~~~
    $ git stash apply@{0}
    ~~~

- 在`dev`分支上修复同样Bug

  - 为了方便操作，Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支

    ~~~
    $ git branch
    * dev
      master
    $ git cherry-pick 3f0e6ff
    ~~~

  - 用`git cherry-pick`，我们就不需要在dev分支上手动再把修bug的过程重复一遍。

### 5. Feature分支

- 功能分支

  - 添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个`feature`分支，在上面开发，完成后，合并，最后，删除该`feature`分支。
  - 一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。

- 删除未合并的分支

  - `feature`分支合并之前，如果删除将丢失修改，此时使用命令：

    ~~~
    $ git branch -d feature
    ~~~

    会发现删除失败。

  - 强行删除，需使用大写的`-D`参数

    ~~~
    $ git branch -D feature
    ~~~

    即可删除成功。

### 6. 多人协作

- 查看远程库

  - 使用`git remote`即可查看远程库的信息

    ~~~
    $ git remote
    ~~~

  - 显示更详细的信息

    ~~~
    $ git remote -v
    ~~~

    会显示了可以抓取和推送的`origin`的地址。如果没有推送权限，就看不到push的地址。

- 推送分支

  - 把该分支上的所有本地提交推送到远程库；推送时，要指定本地分支，例如`master`

    ~~~
    $ git push origin master
    ~~~

  - 若要推送其他分支，如`dev`

    ~~~
    $ git push origin dev
    ~~~

- 抓取分支

  - 当从其他人的远程库clone时，默认情况下，只能看到本地的`master`分支。

  - 现在要在`dev`分支上开发，就必须创建远程`origin`的`dev`分支到本地，用这个命令创建本地`dev`分支：

    ~~~
    $ git checkout -b dev origin/dev
    ~~~

    现在就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程。

- 冲突与解决

  - 此时你已经向`origin/dev`分支推送了他的提交，而碰巧其他人也对同样的文件作了修改，并试图推送。

  - 推送失败，因为你的最新提交和他试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，解决冲突，再推送。

  - `git pull`也失败了，原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接

    ~~~
    $ git branch --set-upstream-to=origin/dev dev
    ~~~

    再pull：

    ~~~
    $ git pull
    ~~~

    这回`git pull`成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push。

  - 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

---

## 六. 标签管理

### 1. 创建标签

- 为某个`commit`打标签

  - 为最新提交的`commit`打标签，先切换到需要打标签的分支上

    ~~~
    $ git branch
    * dev
      master
    $ git checkout master
    ~~~

    使用命令`git tag <name>`打一个新标签

    ~~~
    $ git tag v1.0
    ~~~

    使用`git tag`命令可查看所有标签

    ~~~
    $ git tag
    ~~~

  - 为特定版本打标签，需找到对应版本的`commit id`，如`03b7995...`

    ~~~
    $ git tag v0.9 03b7995
    ~~~

- 查看标签

  - 列出标签

    ~~~
    $ git tag
    ~~~

    注意标签不是按时间顺序列出，而是按字母排序的。

  - 查看标签信息，使用命令`git show <tagname>`

    ~~~
    $ git show v0.9
    ~~~

- 说明

  - 创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字

    ~~~
    $ git tag -a v0.1 -m "version 0.1 released" a2a2898
    ~~~

    用命令`git show <tagname>`可以看到说明文字

    ~~~
    $ git show v0.1
    ~~~

### 2. 操作标签

- 删除本地标签

  - 使用命令`git tag -d <tagname>`删除某个标签

    ~~~
    $ git tag -d v0.1
    ~~~

- 推送标签

  - 推送某个标签，使用命令`git push origin <tagname>`

    ~~~
    $ git push origin v1.0
    ~~~

  - 推送所有尚未推送的标签

    ~~~
    $ git push origin --tags
    ~~~

- 删除远程标签

  - 先从本地删除

    ~~~
    $ git tag -d v0.9
    ~~~

  - 然后从远程删除

    ~~~
    $ git push origin :refs/tags/v0.9
    ~~~

---

> Ps：上次写这么多笔记的时候还是在高中时，虽然Git还有许多我没有见过的功能，但我相信通过不断的努力一定能够熟练掌握Git

> End.Thanks for reading.