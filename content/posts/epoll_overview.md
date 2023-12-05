+++
title = 'epoll_overview'
date = 2023-11-22T10:20:36+08:00
draft = false
+++

## epoll 前世今生
> [IO多路复用](https://mp.weixin.qq.com/s/YdIdoZ_yusVWza1PU7lWaw)
从阻塞IO到异步IO的过程
一切的开始，都起源于这个 read 函数是操作系统提供的，而且是阻塞的，我们叫它 阻塞 IO。
为了破这个局，程序员在用户态通过多线程来防止主线程卡死。
后来操作系统发现这个需求比较大，于是在操作系统层面提供了非阻塞的 read 函数，这样程序员就可以在一个线程内完成多个文件描述符的读取，这就是 非阻塞 IO。
但多个文件描述符的读取就需要遍历，当高并发场景越来越多时，用户态遍历的文件描述符也越来越多，相当于在 while 循环里进行了越来越多的系统调用。
后来操作系统又发现这个场景需求量较大，于是又在操作系统层面提供了这样的遍历文件描述符的机制，这就是 IO 多路复用。
多路复用有三个函数，最开始是 select，然后又发明了 poll 解决了 select 文件描述符的限制，然后又发明了 epoll 解决 select 的三个不足。

## epoll的函数接口
> [epoll如何实现IO多路复用](https://mp.weixin.qq.com/s?__biz=MjM5Njg5NDgwNA==&mid=2247484905&idx=1&sn=a74ed5d7551c4fb80a8abe057405ea5e&chksm=a6e304d291948dc4fd7fe32498daaae715adb5f84ec761c31faf7a6310f4b595f95186647f12&scene=21#wechat_redirect)






