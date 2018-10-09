# **Git基础操作**
1. 新建版本库
- `cd`选择路径
- `mkdir`新建文件夹
- `pwd`查看全路径
- `git init`初始化,将目录变成Git可以管理的仓库
- git仓库中会存在.git的隐藏目录使用`ls -a`参数可以查看
***
2. 文件的添加与新建,在此目录下的文件使用
- `git add filename`将文件添加到暂存区
- `git commit -m “说明内容”`将暂存区文件提交到仓库
- `git status` 查看仓库状态
- `git diff filename` 查看文件的对比(difference) 文件需要未执行add(即只在工作区有效)
- - -
3. 撤销修改
撤销工作区的修改内容
- `git checkout -- filename`撤销相对于版本库或暂存区的内容
撤销暂存区的内容(add操作)
- `git reset HEAD filename`
若执行了commit操作则选择版本回退
- - -
4. 版本回退
- `git log`查看提交历史
- `git log --pretty=oneline`查看缩略信息
- ` git reset --hard HEAD^`在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

- `git reflog`查看历史命令
- - -
5. 恢复最新版本
- `git reset --hard commit_id`
commit_id不用输全
---
6. 删除操作
- `rm`删除本地文件
- `git rm`删除版本库文件(慎用通配符* git可递归通配)
(若本地文件已删除, 使用git rm <file>和git add<file>效果是一样的)
- 将删除操作提交`git commit -m "描述"`
- - -
7. 远程仓库
- 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
- 将本地仓库推送到远端(替换git后内容为仓库地址)
```
$ git remote add origin git@github.com:michaelliao/learngit.git
```
- 推送,将分支本地修改推送到github
```
$ git push origin master
```
- 要关联一个远程库，使用命令
- `git remote add origin git@server-name:path/repo-name.git` 关联后，使用命令
`git push -u origin master`第一次推送master分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
