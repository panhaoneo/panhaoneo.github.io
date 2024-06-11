+++
title = '[转存]centos7.9安装clang'
date = 2024-06-03T09:24:41+08:00
draft = false
tags = ["CentOS", "clang", "编译"]
+++

Title: CentOS 7运行clangd 16_centos7.9安装clang-CSDN博客

URL Source: https://blog.csdn.net/weixin_49758693/article/details/131866414

Markdown Content:
微软官方的VSCode C++插件是单线程模式，在扫描大型工程的时候速度特别慢。所以我一直用vscode-clangd插件。

但在一些比较老的系统上，比如[CentOS](https://so.csdn.net/so/search?q=CentOS&spm=1001.2101.3001.7020) 7，只有glibc 2.17。这会导致新版的clangd无法启动：

    ./bin/clangd: /lib64/libc.so.6: version `GLIBC_2.18' not found (required by ./bin/clangd)
    

CentOS官方源里只有clangd 7，版本太老，无法运行vscode-clangd插件。

我折腾了好几天，试着找到了一种相对简单的方法，**足够让clangd和vscode-clangd插件跑起来，也不破坏系统glibc，也不编译LLVM或GCC**。

本文使用的系统是CentOS 7（VMWare Player 17），clangd版本为[16.0.2](https://github.com/clangd/clangd/releases/tag/16.0.2)。

原理解释
----

> 对原理不感兴趣的可以直接跳过这部分。

我在网上找到的方法大致分为三种：

1.  升级系统的glibc。这种方法比较危险，很容易导致系统无法启动。
2.  自己编译clangd。这需要用cmake 3.x编译LLVM工具链。然而，CentOS 7只自带cmake 2.x。如果要编译的话，首先要升级cmake等工具链。而且自己编译的clangd依然要依赖于glibc，本质上还是没解决问题。
3.  使用容器或虚拟机在CentOS 8里看代码。相当于写代码和跑代码的环境分离，也很不方便。

根据[官方的说法](https://github.com/clangd/vscode-clangd/issues/16#issuecomment-624764721)，clangd不会引入对[glibc](https://so.csdn.net/so/search?q=glibc&spm=1001.2101.3001.7020) 2.17的支持，所以**如果想用官方提供的binary，glibc 2.18是绕不开的。**

但clangd除了glibc 2.18，没有其它的运行库依赖。可以用`ldd`命令列出clangd需要的动态运行库。看上去列出了一大堆，其实都是glibc的库：

    [yaland@localhost clangd_16.0.2]$ ldd -r bin/clangd
    bin/clangd: /lib64/libc.so.6: version `GLIBC_2.18' not found (required by bin/clangd)
    	linux-vdso.so.1 =>  (0x00007ffde5be4000)
    	libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f6cac8ab000)
    	librt.so.1 => /lib64/librt.so.1 (0x00007f6cac6a3000)
    	libdl.so.2 => /lib64/libdl.so.2 (0x00007f6cac49f000)
    	libm.so.6 => /lib64/libm.so.6 (0x00007f6cac19d000)
    	libc.so.6 => /lib64/libc.so.6 (0x00007f6cabdcf000)
    	/lib64/ld-linux-x86-64.so.2 (0x00007f6cacac7000)
    symbol __cxa_thread_atexit_impl, version GLIBC_2.18 not defined in file libc.so.6 with link time reference	(bin/clangd)
    

所以理论上，除了glibc 2.18，其它任何东西都不需要自己重新编译。

单独替换`libc.so`的版本不行。我试过用`LD_LIBRARY_PATH`强制加载新版本的`libc.so`这一个文件，会报一些莫名其妙的错误。因为glibc里的各种库是一个整体，不同版本的是不兼容的。

此外，glibc的库文件搜索路径是编译时写死在代码里的。所以你必须要指定一个目录，把glibc编译和安装进去，它才能正常使用。

因此我的方法是：**编译一个仅用于运行clangd的glibc 2.18，安装到自己的目录里，然后让clangd在运行时动态链接上去。**

执行过程
----

需要安装GCC、GNU make等编译工具。一般这些都是系统自带的。如果没有的话也可以通过`yum`安装。

CentOS 7自带GNU Make 3.82和GCC 4.8.5。

### 编译GLIBC 2.18

注意：本过程**不需要**root权限。

GNU官网下载glibc速度很慢。我这里用的是清华的镜像。

    # 下载
    wget https://mirrors.tuna.tsinghua.edu.cn/gnu/glibc/glibc-2.18.tar.gz
    
    # 解压
    tar -zxf  glibc-2.18.tar.gz
    cd glibc-2.18
    
    # 创建一个build目录方便编译
    mkdir build
    cd build
    
    # prefix选择一个自己的目录
    # glibc之后会被安装到这个目录
    ../configure --prefix=/home/yaland/mylibc
    
    # 编译和安装
    make -j4 && make install
    

你可以验证一下你的glibc是否安装成功：

    # 跳转到你刚才选择的glibc 2.18安装目录
    cd /home/yaland/mylibc/
    
    # 检查glibc版本
    ./bin/ldd --version
    

它应该输出如下内容，显示这是2.18版本：

    ldd (GNU libc) 2.18
    Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
    Written by Roland McGrath and Ulrich Drepper.
    

### 用自己的ld.so运行clangd

在编译好的glibc的`lib`目录下有个`ld-2.18.so`，用它运行clangd：

    /home/yaland/mylibc/lib/ld-2.18.so  /path/to/clangd
    

现在clangd可以正常启动了：

![Image 2: 请添加图片描述](https://img-blog.csdnimg.cn/c9e9444b88e249a88ba37fb79b232216.png)

把这行命令写成可执行的shell脚本，就可以供[VSCode插件](https://so.csdn.net/so/search?q=VSCode%E6%8F%92%E4%BB%B6&spm=1001.2101.3001.7020)使用。类似于：

    #!/usr/bin/env bash
    /path/to/ld-2.18.so /path/to/clangd $@
    

最后加个`$@`是用于展开VSCode传入的命令行参数。

你可以把它命名为`clangd`然后丢到系统的PATH里，也可以随便放到某个目录，然后[到VSCode里设置`clangd.path`](https://stackoverflow.com/questions/51402740/visual-studio-code-clangd-extension-configuration)。

参考文章
----

[GLIBCs not found on host · Issue #16 · clangd/vscode-clangd](https://github.com/clangd/vscode-clangd/issues/16)

[安装clangd：‘GLIBC\_2.18‘ not found解决 - 李响Superb的技术博客 - 51CTO博客](https://blog.51cto.com/u_14013325/4895865)

[Compile and install GLIBC 2.18 in CentOS 7](https://gist.github.com/carlesloriente/ab3387e7d035ed400dc2816873e9089e)

[关于不同版本 glibc 更换的一些问题-Pwn-看雪-安全社区|安全招聘|kanxue.com](https://bbs.kanxue.com/thread-254868.htm)

[c - Can LD\_PRELOAD be used to load different versions of glibc? - Stack Overflow](https://stackoverflow.com/questions/55186770/can-ld-preload-be-used-to-load-different-versions-of-glibc)

[clang - Visual Studio Code clangd extension configuration - Stack Overflow](https://stackoverflow.com/questions/51402740/visual-studio-code-clangd-extension-configuration)