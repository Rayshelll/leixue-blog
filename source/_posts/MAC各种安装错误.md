---
title: MAC各种安装错误
date: 2019-08-15 12:07:58
tags:
---
* `brew install yarn`

    * ERROR:Failed to link all completions, docs and manpages: Permission denied...

    * Solution:`sudo chown -R $USER:admin /usr/local/*`