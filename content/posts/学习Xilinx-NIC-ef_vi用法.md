+++
title = '学习Xilinx NIC Ef_vi用法'
date = 2025-05-28T13:49:55+08:00
draft = true
+++

## 1.ef_vi是啥

| 网卡架构 | 适配器 |
| --- | ----- |
| EF10 | 8000 and X2-series NICs |
| EF100 | SN1000-series SmartNICs |
| EFCT | X3-series NICs (low latency persona) |

ef_vi 允许应用程序直接访问网络适配器数据路径，从而降低延迟并减少每个报文处理开销。它可直接用于需要最低延时发送和接收 API，且不需要 POSIX 套接字接口的应用程序可以直接使用。

## 2.使用场景

### 2.1 sockets 加速

## 3.激活要求

ef_vi 的激活要求取决于所使用的网络适配器：

- 如果使用的是 SFN8000 或 X2 系列适配器，并且需要最快的性能，则必须安装 Onload 或 Plus 激活密钥。
如果没有 Onload 或 Plus 激活密钥，在分配虚拟接口时必须设置 EF_VI_RX_EVENT_MERGE 标志。
分配虚拟接口时必须设置 EF_VI_RX_EVENT_MERGE 标志。这通常会降低性能。
- 如果使用的是 X3 系列适配器，则没有激活要求。