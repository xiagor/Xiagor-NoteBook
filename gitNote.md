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

9. 撤销文件修改（有两种情况）

   + 文件修改保存后还没有被放到暂存区，撤销后就回到版本库一模一样的状态
   + 文件修改保存后已经添加到暂存区，又作了修改，现在，撤销修改就回到添加暂存区后的状态

   `git checkout --<file>`

   