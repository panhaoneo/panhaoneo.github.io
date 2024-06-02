+++
title = '我的C++开发环境'
date = 2024-05-12T13:17:21+08:00
draft = false
+++

vscode + remote + clangd

- 使用介绍
- 安装介绍
- 离线安装
- glic2.18问题 https://blog.csdn.net/weixin_49758693/article/details/131866414


makefile 生成clangd compile_commands.json [how-to-turn-makefile-into-json-compilation-database](https://stackoverflow.com/questions/21134120/how-to-turn-makefile-into-json-compilation-database)
```
make --always-make --dry-run \
 | grep -wE 'gcc|g\+\+' \
 | grep -w '\-c' \
 | jq -nR '[inputs|{directory:".", command:., file: match(" [^ ]+$").string[1:]}]' \
 > compile_commands.json
```