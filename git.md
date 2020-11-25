## 目录

<!-- TOC -->

- [目录](#目录)
- [简单的学习](#简单的学习)
- [git命令](#git命令)
  - [查看git文件状态：status](#查看git文件状态status)
  - [git配置：config](#git配置config)
  - [分支管理：branch、checkout、merge](#分支管理branchcheckoutmerge)
  - [fetch指令？](#fetch指令)
  - [花式撤销：reset](#花式撤销reset)
  - [状态查询：reflog、log](#状态查询refloglog)
  - [文档查询：help](#文档查询help)
  - [文件暂存：stash](#文件暂存stash)
  - [差异比较：diff](#差异比较diff)
- [分支命令](#分支命令)
- [多人协作](#多人协作)
- [常见问题](#常见问题)

<!-- /TOC -->



## 简单的学习

1. 创建git仓库：

   `git init`

2. 添加文件、提交文件：

   `git add <file>` or `git add .`（这个是添加全部修改的文件）

   `git commit -m "message"`

3. 查看commit提交历史（最近到最远的提交日志）

   `git log`

4. 回退到上一个版本

   `git reset --hard HEAD^`

5. 回退到上上一个版本

   `git reset --hard HEAD^^`

6. 回退到指定某一个commit版本

   `git reset --hard <commitId>`

7. 查看命令历史（当回退版本后又想恢复到新版本时

   `git reflog`

8. 查看状态（add是把要提交的修改文件放到暂存区，commit可以一次性把暂存区的所有修改提交到分支）

   `git status`

9. 撤销文件修改，有两种情况（不是撤销commit）

   + 文件修改保存后还没有被放到暂存区，撤销后就回到版本库一模一样的状态
   + 文件修改保存后已经添加到暂存区，又作了修改，现在，撤销修改就回到添加暂存区后的状态

   `git checkout -- <file>`（-- 和file之间有空格）

   小结：

   ​	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，直接用命令：

   `git checkout -- file`。

   ​	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步：

   第一步用命令：`git reset HEAD <file>`回退到场景1（就是修改文件并保存但是没有添加到暂存区的场景），再按场景1操作。

   ​	场景3：：已经提交了不合适的修改到版本库时，想要撤销本次提交，要用版本退回的一系列操作（前提是没有推送到远程库）

10. 添加远程库

    1. 查看用户主目录（系统盘的Administrator）下有没有.ssh目录，如果有，再看里面是否有id_rsa和id_rsa.pub这两个文件，如果没有则需创建：

       `ssh-keygen -t rsa -C "yourEmail@qq.com"`

       然后一路回车，就会自动创建这两个文件，分别是密钥对的私钥和公钥

    2. 在GitHub中添加公钥的内容

       ![](Images/git/2230)

    3. 先在github上建一个空仓库，注意不要勾选readme初始化

    4. 运行下面命令，让本地库与远程库关联起来

       `git remote add origin git@github.com:github账户名/仓库名.git` 

    5. 关联成功后用如下命令把本地内容推动到远程库，其中-u是指定后面的仓库名和分支名为默认，以后直接用`git push`即可

    6. 如果远程库已经存在readme文件，这时会报错，提醒你需要pull下来，命令如下

       `git pull origin master`

       这时又会报错：` fatal: refusing to merge unrelated histories`

       说这两个库的git历史记录不相干而无法合并，这时我们可以在后面加上一个参数即可：

       `  git pull origin master --allow-unrelated-histories `

11. 从远程库克隆

    `git clone 仓库地址 `



其他的暂时不学了，实习的时候有用到合并分支，现在暂时用不到，git就学到这里，方便自己学习就行。

------



## git命令

### 查看git文件状态：status

- 通常我们需要查看一个文件的状态

  ```
  git status
  ```



### git配置：config

![img](Images/git/29f0c70414b14fe1986b376f7b303959~tplv-k3u1fbpfcp-zoom-1.image)

+ 列出当前配置

  ```
  git config --list
  ```

+ 列出Repository配置

  ```
  git config --local --list
  ```

+ 列出全局配置

  ```
  git config --global --list
  ```

+ 列出系统配置

  ```
  git config --system --list
  ```

+ 配置用户名

  ```
  git config --global user.name "your name"
  ```

+ 配置用户邮箱

  ```
  git config --global user.email "youremail@excample.com"
  ```



### 分支管理：branch、checkout、merge

+ 补充：将某个分支的修改合并到当前分支！

  （一般用于在某个分支的小改动，切换到另外一个分支的时候想在当前的分支合并这个小改动）

  ```
  git cherry-pick <commit ID>
  ```

  

![img](Images/git/3bff7ddbc6a145f993c0841eb81c8998~tplv-k3u1fbpfcp-zoom-1.image)

+ 查看本地分支

  ```
  git branch
  ```

+ 查看远程分支

  ```
  git branch --remote
  ```

+ 查看本地和远程分支

  ```
  git branch --all
  ```

+ 从当前分支，切换到其他已有分支

  ```
  git checkout <branch-name>
  //举个例子
  git checkout feature/test
  ```

+ 创建并切换到新分支

  ```
  git checkout -b <branch-name>
  //举个例子
  git checkout -b feature/test
  //相当于
  //新建分支git branch feature/test
  //再切换分支git checkout feature/test
  ```
  
+ 删除分支

  ```
  git branch --delete <branch-name>
  //举个例子
  git branch --delete feature/test
  ```

+ 当前分支与指定分支合并

  ```
  git merge <branch-name>
  // 举个例子👇
  git merge feature/test
  ```

  > 合并有可能有发生冲突，此时需要手动解决冲突的代码
  >
  > 然后再执行`git commit -a`

+ 查看分支的合并情况

  ```
  git log --graph --pretty=oneline --abbrev-commit
  ```

+ 查看哪些分支已经合并到当前分支

  ```
  git branch --merged
  ```

+ 查看哪些分支没有合并到当前分支

  ```
  git branch --no-merged
  ```

+ 查看各个分支最后一个提交对象的信息

  ```
  git branch --verbose
  ```

+ 删除远程分支

  ```
  git push origin --delete <branch-name>
  ```

+ 重命名分支

  ```
  git branch --move <oldbranch-name> <newbranch-name>
  ```

+ 拉取远程分支并创建本地分支

  ```
  git checkout -b 本地分支名x origin/远程分支名x
  
  // 另外一种方式,也可以完成这个操作。
  git fetch origin <branch-name>:<local-branch-name>
  // fetch这个指令的话,后续会梳理
  ```








### fetch指令？

![img](Images/git/6c666ec139fe4dc5a08df6b811b9803d~tplv-k3u1fbpfcp-zoom-1.image)



### 花式撤销：reset

![img](Images/git/f29320c710544828a494918b1ec2da05~tplv-k3u1fbpfcp-zoom-1.image)

+ 撤销**工作区**修改（就是在工作区修改了某个文件并保存了，然后突然不想要修改的内容了，放弃更改的代码）

  ```
  git checkout -- <file>
  ```

+ 暂存区文件撤销（不覆盖工作区，也就是撤销了暂存区，但是工作区的文件还在并被保存，即回到`git add <file>`操作前的状态）

  ```
  git reset HEAD <file>
  ```

+ 版本回退（每提交一次到本地仓库都是一个版本）

  ```
  //丢弃最新提交（未提交的内容会被擦掉），回到上一个版本
  git reset --hard HEAD^                   
  //丢弃最新提交（未提交的内容不会被擦掉），回到上一个版本
  git reset --soft HEAD^
  // 回退到某一个commit id（可通过reflog或log查看id，同样未提交的内容会被删掉）
  git reset --hard <commitId>
  ```

+ 总结：

  ​	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，直接用命令：

  `git checkout -- file`。

  ​	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步：

  第一步用命令：`git reset HEAD <file>`回退到场景1（就是修改文件并保存但是没有添加到暂存区的场景），再按场景1操作。

  ​	场景3：：已经提交了不合适的修改到版本库时，想要撤销本次提交，要用版本退回的一系列操作（前提是没有推送到远程库）



### 状态查询：reflog、log

+ 查看状态

  ```
  git status
  ```

+ 查看历史操作记录

  ```
  git reflog
  ```

+ 查看日志

  ```
  git log
  ```



### 文档查询：help

+ 展示Git命令大纲

  ```
  git help
  ```

+ 展示Git命令大纲全部列表

  ```
  git help -a
  ```



### 文件暂存：stash

![img](Images/git/1b229cb4872e4991b33181cdad72b59d~tplv-k3u1fbpfcp-zoom-1.image)

+ 查看stash列表

  ```
  git stash list
  ```

+ 暂存代码

  ```
  git stash save "备注"
  ```

+ 恢复某条stash的代码

  ```
  git stash pop stash@{ID}
  //如果是恢复stash@{0}的话可省略
  ```

+ 删除某个stash暂存

  ```
  git stash drop stash@{ID}
  ```


+ 删除全部stash

  ```
  git stash clear
  ```

  

### 差异比较：diff

![img](Images/git/c779e736198247bfb0795b50dced0814~tplv-k3u1fbpfcp-zoom-1.image)



Creating a new branch is not quick!


Creating a new branch is quick and simple.

我正在开发新任务哦！！！！！



## 分支命令

![img](Images/git/fd8abe5e5605411d8dbe5c4faa0054aa~tplv-k3u1fbpfcp-zoom-1.image)



## 多人协作

多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。



## 常见问题

[常见问题以及解决办法](https://juejin.cn/post/6891146425590087693#heading-5) 

+ `git merge` 会新建一个新的 commit 对象，然后两个分支以前的 commit 记录都**指向这个新 commit 记录**。这种方法会
  **保留**之前每个分支的 commit 历史。

  `git rebase` 会先找到两个分支的第一个**共同的 commit 祖先**记录，然后将提取当前分支这之后的所有 commit 记录，然后
  将这个 commit 记录**添加到目标分支的最新提交后面**。经过这个合并后，两个分支合并后的 commit 记录就变为了线性的记
  录了。（会修改之前 commit 的记录）

+ `git fetch`就是将远程代码同步到**本地仓库记录的远程分支**(remotes文件的Origin/master)，

  `git pull`是直接同步到**当前分支**也就是**本地分支**(heads文件夹的master)（可能会有冲突）

