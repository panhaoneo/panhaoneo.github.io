+++
title = 'Git的https和ssh'
date = 2024-05-24T15:19:26+08:00
draft = false
tags = ["git"]
+++


设置以下的命令，可以在一次输入密码之后，保存密码到本地.git-credentials
```
git config --global credential.helper 'store'
```


ssh方式设置的是密钥