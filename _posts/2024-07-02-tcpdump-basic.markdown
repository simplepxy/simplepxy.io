---
layout: post
title:  "tcpdump在android抓包中的使用"
date:   2024-07-01 20:35:00 +0800
categories: android tcp
---

如果想要抓取app生产环境下的网络包，一般只能使用例如`fiddler`等工具的代理能力才能实现。但是如果你有一台`root`过的设备，就可以直接通过`tcpdump`工具来直接抓取设备上的网络请求,并配合`wireshake`查看设备上的网络请求。

1. 首先要去https://www.androidtcpdump.com/android-tcpdump/downloads下载已经预编译好的`tcpdump`的包，当然你也可以自己编译，官网上有详细的编译指南，这里不做赘述。
2. 把`tcpdump`放到`/data/local/`目录下，并且设置`777`的权限。
3. 切换到/data/local/目录下，执行命令 `tcpdump -i any -p -vv -s 0 -w capture.pcap` 开始抓包
4. 设备操作完毕之后，把`capture.pcap`拖到电脑中使用`wireshake`工具查看

`tcpdump`的参数使用可以参考如下：

https://www.tcpdump.org/manpages/tcpdump.1.html

https://www.cnblogs.com/wongbingming/p/13212306.html