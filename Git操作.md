# **使用git bash打开**
1. 新建版本库
- cd选择路径
- mkdir新建文件夹
- pwd查看全路径
- git init初始化,将目录变成Git可以管理的仓库
- git仓库中会存在.git的隐藏目录使用ls -a参数可以查看
2. 文件的添加与新建,在此目录下的文件使用
- git add filename将文件添加到暂存区
- git commit -m “说明内容”将暂存区文件提交到仓库
- git status 查看仓库状态
- git diff filename 查看文件的对比(difference) 文件需要未执行add(即只在工作区有效)
3. 撤销修改
撤销工作区的修改内容
- git checkout -- filename撤销相对于版本库或暂存区的内容
撤销暂存区的内容(add操作)
- git reset HEAD filename
若执行了commit操作则选择版本回退

4. 版本回退
- git log查看提交历史
- git log --pretty=oneline查看缩略信息
在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

- git reset --hard HEAD^

- git reflog查看历史命令
5. 恢复最新版本
- git reset --hard commit_id
commit_id不用输全
6. 删除操作
- rm删除本地文件
- git rm删除版本库文件
(若本地文件已删除, 使用git rm <file>和git add<file>效果是一样的)
- 将删除操作提交git commit -m "描述"
