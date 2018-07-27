## 关于解决github fork 项目更新的解决方案

#### 问题描述:

**//当我们在github上fork某个项目后，当原项目更新后，我们需要更新自己的fork分支，使自己的分支与源分支保持同步**

#### 解决方案:

```shell
# 1. clone 自己的 fork 分支到本地;可以直接使用 GitHub 客户端，clone 到本地，如果使用命令行，命令为：
$ git clone git@github.com:morethink/git-recipes.git
# 2. 进入仓库，增加源分支地址到你项目远程分支列表中;此处是关键，先得将原来的仓库指定为 upstream，命令为：
$ git remote add upstream git@github.com:geeeeeeeeek/git-recipes.git
# 3. 此处可使用 git remote -v 查看远程分支列表
$ git remote -v origin git@github.com:morethink/git-recipes.git (fetch) origin git@github.com:morethink/git-recipes.git (push) upstream git@github.com:geeeeeeeeek/git-recipes.git (fetch) upstream git@github.com:geeeeeeeeek/git-recipes.git (push)
# 4. fetch 源分支的新版本到本地
$ git fetch upstream
# 5. 切换到本地master分支
$ git checkout master
# 6. 合并两个版本的代码
$ git merge upstream/master
# 7. 将合并后的代码 push 到 GitHub 上去
$ git push origin master
```
