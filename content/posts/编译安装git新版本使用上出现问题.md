+++
title = '编译安装git新版本使用上出现问题'
date = 2024-05-22T10:57:52+08:00
draft = false
+++

在centos上编译安装git2.45.1,然后再使用的时候报错：`git: 'remote-https' is not a git command. See 'git --help'`,查找一个解决办法是`export PATH=$PATH:/usr/local/libexec/git-core`,但是不能解决。

最终看到一个说是git新版使用libcurl

```
Git使用libcurl库通过http://和https://.推送/获取存储库。如果在不存在库的情况下编译git，则会发生此错误。

安装它(yum/dnf install libcurl-devel)，然后重新配置和重新编译git。应该管用的。

链接：https://github.com/git/git/blob/b896f729e240d250cf56899e6a0073f6aa469f5d/INSTALL#L141-L149
```