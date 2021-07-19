---
title: UnriadNAS折腾记录
date: 2021-07-19 20:23:00 +0800
categories: [记录]
tags: [unraid,docker,nas]
---

前几天朋友低价转手给我一个全新8TB的希捷SMR盘，于是就开始折腾起了NAS。

## 安装于初始设置

### 制作启动盘

没有什么难度，基本按照[官网的教程](https://wiki.unraid.net/Articles/Getting_Started#Getting_Started)走就行。  
只讲重点。  

1. 用质量好点的U盘，假冒伪劣产品有可能没序列号导致无法使用。
1. [Unraid官网下载USB Creator](https://unraid.net/download)。想白嫖也可以去找找开心版。
1. 用USB Creator把Unraid系统刷进U盘。
1. 插上主板，开机。
1. 尝试默认的本地域名`http://tower`/`http://tower.local`，又或者是通过路由器或者局域网扫描找到Unraid的IP。
1. 默认是root用户没密码直接就能进，进去之后立刻设置密码。
1. 进去之后激活KEY，或者先试用30天。

### 特殊准备

为了之后安装各种社区应用，先把`hosts`改了，并写进go文件里，这样就能开机自动改。  

```shell
nano /etc/hosts
```

```txt
199.232.28.133  raw.githubusercontent.com
199.232.4.133   raw.githubusercontent.com
199.232.4.133   raw.github.com
```

```shell
nano /boot/config/go
```

```shell
echo "199.232.28.133  raw.githubusercontent.com" >> /etc/hosts
echo "199.232.4.133   raw.githubusercontent.com" >> /etc/hosts
echo "199.232.4.133   raw.github.com" >> /etc/hosts
```

### 安装社区应用插件

论坛帖：<https://forums.unraid.net/topic/38582-plug-in-community-applications/>  
通过安装社区插件来让Unraid内置社区插件浏览功能。  

`https://raw.githubusercontent.com/Squidly271/community.applications/master/plugins/community.applications.plg`  

### Unassigned Devices

论坛贴：<https://forums.unraid.net/topic/92462-unassigned-devices-managing-disk-drives-and-remote-shares-outside-of-the-unraid-array/>  
基本上是必备插件，可以识别各种文件系统的储存设备，比如刚从Windows上拆下来的NTFS的盘，这样就能拷进整列里了。  

`https://github.com/dlandon/unassigned.devices/raw/master/unassigned.devices.plg`  
