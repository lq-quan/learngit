# #3 Linux / WSL

---

> 本文档为本人选择任务1的截图与文字说明

### 1.启用WSL

- 打开电脑的**控制面板**，选择**程序**，选择**程序和功能**下方的**启用或关闭Windows功能**

  ![启用或关闭Windows功能](https://github.com/lq-quan/WSL-Screenshots/raw/main/1.png)

- 勾选：

  - **适用于Linux的Windows子系统**

  - **虚拟机平台**

    ![勾选条目](https://github.com/lq-quan/WSL-Screenshots/raw/main/2.png)

- 重新启动Windows。

### 2. 升级到WSL2

- 搜索并下载`wsl_update_x64.msi`，并进行安装

  ![下载与安装升级文件](https://github.com/lq-quan/WSL-Screenshots/raw/main/3.png)

- 根据进程及实际需要安装

  ![安装](https://github.com/lq-quan/WSL-Screenshots/raw/main/4.png)

- 安装好后，**用管理员身份运行**`Powershell`

  ![Powershell](https://github.com/lq-quan/WSL-Screenshots/raw/main/5.png)

- 输入以下命令：

  ![输入命令](https://github.com/lq-quan/WSL-Screenshots/raw/main/6.png)

### 3. 在WSL中安装Ubuntu

- 在启用了WSL后，打开**Windows Store**，搜索**Ubuntu**

  ![搜索Ubuntu](https://github.com/lq-quan/WSL-Screenshots/raw/main/7.png)

- 建议选择最新版本的**Ubuntu 22.04 LTS**，点击**获取**

  ![获取](https://github.com/lq-quan/WSL-Screenshots/raw/main/8.png)

- 随后便是下载和安装的过程

  ![下载安装](https://github.com/lq-quan/WSL-Screenshots/raw/main/9.png)

- 完成后，打开**Ubuntu终端**，创建账户

  ![创建账户](https://github.com/lq-quan/WSL-Screenshots/raw/main/10.png)

- Linux系统需要不定时更新。更新时，需要从远端服务器下载更新包。 Linux系统更新需要一个更新源配置文件**sources.list**，为加速下载，需要将服务器改为国内的镜像，例如清华大学的**tuna镜像网站**。

- 打开VS Code，复制粘贴以下文字：

  ![更新包](https://github.com/lq-quan/WSL-Screenshots/raw/main/11.png)

- 在Ubuntu中替换`sources.list`：在终端中输入以下文字

  ![替换文件](https://github.com/lq-quan/WSL-Screenshots/raw/main/12.png)

- 更新Ubuntu：在终端中发出如下命令

  ![更新](https://github.com/lq-quan/WSL-Screenshots/raw/main/13.png)

- 升级Upgrade：在终端中发出以下命令

  ![升级](https://github.com/lq-quan/WSL-Screenshots/raw/main/14.png)

> 至此，WSL的Ubuntu发行版配置完成。

---

### 4. 将VS Code连接至WSL2

- 进入VS Code，搜索并安装好`remote`插件

  ![remote](https://github.com/lq-quan/WSL-Screenshots/raw/main/15.png)

- 在Code中远程连接Ubuntu：点击左边类似如下图标（远程连接图标）

  ![图标](https://github.com/lq-quan/WSL-Screenshots/raw/main/16.png)

- 将鼠标放到**Ubuntu 22.04 LTS**标题上，出现了一个有加号的目录图标，点击它

  ![WSL2](https://github.com/lq-quan/WSL-Screenshots/raw/main/17.png)

- 此后Code会打开一个新窗口，点击`Open Folder`，并输入创建好的目录名如`test`。

- 创建工作目录，我们的登录账户为普通账户`86157`，在终端中输入以下命令创建工作目录

  ![创建工作目录](https://github.com/lq-quan/WSL-Screenshots/raw/main/18.png)

  此后，用户`86157`对目录`test`拥有了完全的读写控制

> 至此，我们已将VS Code连接至我们的WSL2 Ubuntu。

---

### 5. 一些感想

- 好奇心是科学之母。在此之前，我自认为对计算机有一定的了解，所以走一遍上面的所有的流程于我而言没有过于困难的地方。但实际上，我无从得知上面的一些流程或者命令从何而来，有什么作用，或者为什么要这么做。教程或者搜索引擎让我这么做，但我想了解一些更为深入的知识，依靠搜索引擎或者是优秀的提问可以让我们短时间内对某个问题有一定的了解与把控，此后我们需要更加长时间的复习，或是实践。
- 实践才是检验真理的唯一标准。未来的我可能会对代码中类似于Bug的修复感到困惑，此时仅仅在脑海中空想该如何去修复这个Bug显然是低效的，或是行不通的。我们可以在编辑软件中多多实践我们脑海中想出来的某个办法，键盘也许是死的，但是你可以利用它创造出一些意想不到的结果或效果。今后多多敲动手中的键盘吧，它会给你惊喜！遇到没有头绪的问题的话，也许可以借助一些外力，包括但不限于搜索引擎或提问。但在提问之前多多利用搜索引擎，也许会省下更多时间！
- 世上无难事，只怕有心人。在尝试完成这道题之前，我认为这个题对我而言也许是我做不到的，第一眼看上去有那么多不认识的名词或英文单词。但当时的我可能不会想到我会走到现在这一步，也许我现在对我自己或者这个世界有了一些改观：有些事情可能没有想象中的那么难，只要我们愿意去尝试，相信许多问题都会迎刃而解！

> End. Thanks for reading.