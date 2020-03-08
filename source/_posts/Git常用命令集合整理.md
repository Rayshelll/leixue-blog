---
title: Git常用命令集合整理
date: 2019-08-08 18:02:44
tags: 
- Git
---
`git init` 初始化项目

`git config --global user.name "Your Name"` 配置名字

`git config --global user.email "email@example.com"` 配置邮箱

`git add <file>`、`git add .` 将修改文件放入暂存区

`git commit -m "xx"` 提交文件到版本库里

`git status` 查看当前文件状态

`git diff file/id` 看出文件或提交的不同

`git log` 打印log信息

`git reset --hard HEAD^/id` 回退到最初版本或是指定commit id版本

`git reflog` 查看所有分支的所有操作记录

`rm file` 删除文件

`git remote add origin xxx` 关联远程仓库

`git remote rm origin` 移除远程仓库关联

`git remote -v` 查看远程仓库信息

`git clone 地址` 克隆仓库

`git pull` 拉取代码

`git pull —rebase` 拉取并rebase

`git push -u origin master` 第一次提交代码到远程仓库

`git push origin feature/VouncherModified  -f` 强推代码到远端仓库，本地覆盖远端分支

`git push --set-upstream origin feature/B4MWeightModified` push到远端分支

`git branch b1` 创建本地分支

`git checkout b1` 切换本地分支

`git checkout -b b1` 创建并切换本地分支

`git branch` 查看本地分支

`git branch -d b1` 删除本地分支

`git merge ba` 合并分支

`git checkout -b b1 origin/b1`  拉取远程分支b1到本地分支b1

`git branch —set-upstream b1 origin/b1` 本地分支关联远端分支

`git branch -D b1` 删除本地分支

`git push origin --delete b1` 删除远端分支

`git stash` 将修改文件放入暂存里

`git stash list` 查看暂存列表

`git stash pop/apply` 取出暂存文件

`git stash drop` 删除暂存

`git stash pop stash@{0}` 取出第几个暂存

`git rebase origin/master` rebase 远程master分支（rebase的意思是将自己修改的文件放到基于master最新修改上）

`git rebase —continue` 解决修改冲突后，继续rebase

`git rebase b1` rebase 分支b1

`git reset [提交ID]` 回退，软回退

`git reset --hard [提交ID]` 强回退，直接全部会回退到某个版本，源码也回退到这个版本

`git reset --soft [提交ID]` 软回退，回退了commit的信息，源码不变

`git revert [提交ID]` 是用一次新的commit来回滚之前的commit

#### `git merge` 和 `git rebase` 的不同

``` js
// git rebase 过程
git rebase origin master
修改内容
git add .
git rebase --continue

// git merge 过程
git fetch
git merge
处理冲突
git add  .
git push
```
什么时候我应该用git merge?
所有提交历史都保留，想要保存项目完整的历史，并且避免重写公共分支上的commit，使用git merge
什么时候我应该用git rebase?
丢弃原始提交，形成线性提交历史，想要一个干净的、线性的提交历史，没有不必要的合并提交，使用 git rebase
1. 不能在公共分支上使用它。比如master，develop。
2. 通常用在你自己的独享分支上。