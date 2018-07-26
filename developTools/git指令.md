### git 指令进阶

* git branch -vv ---查看本地分支关联（跟踪）的远程分支之间的对应关系

* git push <远程主机名> <本地分支名>:<远程分支名> --- git push的完成操作命令, 其中当远程分支跟本地分支有追踪关系时，远程分支可以省略，
所以git push origin master中的 master 指的是本地的master分支

* git remote update <远程仓库名> --- 用于更新远程仓库的所有分支信息
eg. 如果在github中新增加了远程分支，此时可以通过git remote update origin更新本地git仓库的远程仓库分支信息

* git checkout -b 本地分支名 origin/远程分支名  ----- 将远程git仓库里的指定分支拉取到本地（本地不存在的分支）

* git add -A ----stage所有的文件(包括已删除的文件), git add . ----stage新增的和修改的文件
所以当远程仓库增加了某些不需要的文件和文件夹时，先通过 git add -A stage 后 git commit --->git push 操作可以删除远程git仓库中不需要的文件

* git diff --cached  比较暂存区和HEAD的文件差异

* git  log  --stat  查看提交历史记录, 其中--stat会显示文件的历史变化

* git diff   比较差异 

* git log --pretty = oneline

* git status -s  精简指令

* git  reset HEAD 用repo中的内容重写stage中的内容，工作区

* git rm --cached <file> 直接从暂存区删除文件, 工作区不做变化

* git checkout . 删除工作区的内容

* git revert 和 git reset ，git checkout

* git checkout HEAD^ // checkout 到 上一个commit,然后调用git checkout master 回到当前分支; [没搞懂]

* git reset --soft(默认为 git reset) 和 git reset --hard  // soft 会把撤销的提交保存到暂存区index中; hard 会直接撤销到前一步

* git revert --continue  // revert 生成带默认message的commit。

* git revert  <commit ID> --no-commit  回滚并默认不生成新的commit
