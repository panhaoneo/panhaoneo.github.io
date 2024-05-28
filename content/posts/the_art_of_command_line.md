+++
title = 'The_art_of_command_line'
date = 2024-05-21T16:58:28+08:00
draft = false
+++

> 参考[the art of command line in github](https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md)
> 和自己的之前的积累

- 定时记录top的命令
`watch -n 1 "top -b -d 1 -n 1 >> mem.log"`

- find 命令  和xargs
`find . -type f | xargs grep ...`

- for fun: 查看自己history中排名前十的命令
`history | awk '{CMD[$2]++;count++;} END { for (a in CMD )print CMD[ a ]" " CMD[ a ]/count*100 "% " a }' | grep -v "./" | column -c3 -s " " -t |sort -nr | nl | head -n10`

- tcpdump常用命令
`tcpdump -i eth0 port 58298 -s 0 -X`
`tcpdump –i any –X –v –vv tcp and dst port 6379`


-   在 Bash 中，变量有许多的扩展方式。`${name:?error message}` 用于检查变量是否存在。此外，当 Bash 脚本只需要一个参数时，可以使用这样的代码 `input_file=${1:?usage: $0 input_file}`。在变量为空时使用默认值：`${name:-default}`。如果你要在之前的例子中再加一个（可选的）参数，可以使用类似这样的代码 `output_file=${2:-logfile}`，如果省略了 `$2`，它的值就为空，于是 `output_file` 就会被设为 `logfile`。数学表达式：`i=$(( (i + 1) % 5 ))`。序列：`{1..10}`。截断字符串：`${var%suffix}` 和 `${var#prefix}`。例如，假设 `var=foo.pdf`，那么 `echo ${var%.pdf}.txt` 将输出 `foo.txt`。

- 使用括号扩展（`{`...`}`）来减少输入相似文本，并自动化文本组合。这在某些情况下会很有用，例如 `mv foo.{txt,pdf} some-dir`（同时移动两个文件），`cp somefile{,.bak}`（会被扩展成 `cp somefile somefile.bak`）或者 `mkdir -p test-{a,b,c}/subtest-{1,2,3}`（会被扩展成所有可能的组合，并创建一个目录树）。

-   通过使用 `<(some command)` 可以将输出视为文件。例如，对比本地文件 `/etc/hosts` 和一个远程文件：
      `diff /etc/hosts <(ssh somehost cat /etc/hosts)`

-   使用 [`ag`](https://github.com/ggreer/the_silver_searcher) 在源代码或数据文件里检索（`grep -r` 同样可以做到，但相比之下 `ag` 更加先进）。

-   Markdown，HTML，以及所有文档格式之间的转换，试试 [`pandoc`](http://pandoc.org/)。

-   当你要处理棘手的 XML 时候，`xmlstarlet` 算是上古时代流传下来的神器。
    
-   使用 [`jq`](http://stedolan.github.io/jq/) 处理 JSON。
    
-   使用 [`shyaml`](https://github.com/0k/shyaml) 处理 YAML。


