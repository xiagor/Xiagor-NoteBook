1. 创建git仓库：

   `git init`

2. 添加文件、提交文件：

   `git add <file>` or `git add .`（这个是添加全部修改的文件）

   `git commit -m "message"`

3. 查看版本库的状态（最近到最远的提交日志）

   `git log`

4. 回退到上一个版本

   `git reset --hard HEAD^`

5. 回退到上上一个版本

   `git reset --hard HEAD^^`

6. 回退到指定某一个commit版本

   `git reset --hard <commitId>`

7. 查看每一次命令记录（当回退版本后又想恢复到新版本时

   `git reflog`

8. 我来试试！