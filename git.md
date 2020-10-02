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

       ![](http://note.youdao.com/yws/public/resource/4653994abae090b764e7fb65a039a7fe/xmlnote/9375B3E1383A489395F26E601FD6F16B/2230)

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