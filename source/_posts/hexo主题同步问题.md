---
title: hexo主题同步问题
date: 2019-08-29 16:17:38
tags:
---
目前hexo主题都是通过git clone的方式克隆到本地来的，然而在提交站点源码到远程仓库时，themes文件夹下的主题文件是不会提交到仓库里的，因此我们如果更改了主题文件下的一些设置，这部分设置由于没有提交会被丢失，这带来了极大的不便。为此，我们决定采用官方推荐的`fork+subtree`的方式来管理主题。
1. 删除themes目录下的next文件夹，并将修改push到github
``` git
git add .
git commit -m "delete next"
git push
```
2. 进入next的[github主页](https://github.com/iissnan/hexo-theme-next)，`fork`一下，在自己的GitHub仓库生成hexo-theme-next仓库

3. 待fork完成后绑定next主题为子项目
``` git
git remote add -f next git@github.com:Rayshelll/hexo-theme-next.git
git subtree add --prefix=themes/next next master --squash
```

4. 更新子项目
``` git
git fetch next master
git subtree pull --prefix=themes/next next master --squash
```

5. 从子目录push到远程仓库  
``` git
git subtree push --prefix=themes/next next master
```