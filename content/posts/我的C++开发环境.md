+++
title = '我的C++开发环境'
date = 2024-05-12T13:17:21+08:00
draft = false
tags = ["C++"]
+++

## 开发场景一：macbook + 远程内网linux开发

### vscode 配置

插件列表：clangd,cmake,remote-ssh,gitlens,copilot/continue,vscode-icons,GDB Debug

1. clangd 
- 安装clangd-server
centos8/ubuntu20.04 可以直接安装新版本,参考[clangd page](https://clangd.llvm.org/)。

centos7则需要单独编译安装一套glic2.18以上的库。参考[这里](https://blog.csdn.net/weixin_49758693/article/details/131866414)。

- vscode配置
``` json
"clangd.arguments": [
        "--log=verbose",
        "--header-insertion=iwyu",
        "--pch-storage=memory",
        "--function-arg-placeholders=false",
        "--background-index",
        "--clang-tidy",
        "-j=12",
      ],
"clangd.path": "/path/to/clangd",
```



remote + github copilot + 离线
https://github.com/orgs/community/discussions/6942

"remote.extensionKind": {
    "GitHub.copilot": ["ui"],
    "GitHub.copilot-chat": ["ui"],
    "linhmtran168.mac-ca-vscode": ["ui"],
}

Here's why it works: https://code.visualstudio.com/api/advanced-topics/extension-host

2. cmake-tools
