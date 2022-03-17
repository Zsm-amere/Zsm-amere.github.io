---
layout:     post
title:      树莓派安装 QtWebEngine 环境
subtitle:   树莓派4B-Qt5 安装 QtWebEngine 环境
date:       2022-03-16
author:     AMERE
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Qt
    - 树莓派
---

# 在树莓派中安装 Qt5 WebEngine 模块

## 1、准备工作

1. 查看系统版本

   > ```shell
   > lsb_release -a
   > ```
   >
   > ![View respberry system version](https://tva4.sinaimg.cn/large/006sqMpgly1h0cwvy4s6pj30da03qjsx.jpg)

2. 查看 Qt 版本

   > ```shell
   > qmake -v
   > ```
   >
   > ![View qt version](https://tva2.sinaimg.cn/large/006sqMpgly1h0cxl7uh38j30fn01rjs8.jpg)

3. 查找下载安装包

   访问树莓派官方系统[软件包]([Debian -- "bullseye" 版面列表](https://packages.debian.org/stable/))网站，选择对应的系统版面列表，或者在搜索页面直接搜索相应的包，选择下载

   ![raspberry packages](https://tva2.sinaimg.cn/large/006sqMpgly1h0cxtc05bsj31ha0pntpm.jpg)

   > 下载对应的 `armhf` 版本
   >
   > 1. [libqt5webenginecore5_5.11.3+dfsg-2+deb10u1_armhf.deb](https://packages.debian.org/buster/libqt5webenginecore5)
   > 2. [libqt5webengine5_5.11.3+dfsg-2+deb10u1_armhf.deb](https://packages.debian.org/buster/libqt5webengine5)
   > 3. [libqt5webenginewidgets5_5.11.3+dfsg-2+deb10u1_armhf.deb](https://packages.debian.org/buster/libqt5webenginewidgets5)
   > 4. [qtwebengine5-dev_5.11.3+dfsg-2+deb10u1_armhf.deb](https://packages.debian.org/buster/qtwebengine5-dev)

   > ```shell
   > sudo dpkg -i libqt5webenginecore5_5.11.3+dfsg-2+deb10u1_armhf.deb
   > sudo dpkg -i libqt5webengine5_5.11.3+dfsg-2+deb10u1_armhf.deb
   > sudo dpkg -i libqt5webenginewidgets5_5.11.3+dfsg-2+deb10u1_armhf.deb
   > sudo dpkg -i qtwebengine5-dev_5.11.3+dfsg-2+deb10u1_armhf.deb
   > ```

## 2、安装

在提示 `dependency problems- leaving unconfigured` 错误时，运行

> ```shell
> sudo apt-get -f install
> ```

## 3、硬件加速相关配置

> ```shell
> sudo apt-get install libgles2-mesa libgles2-mesa-dev xorg-dev
> ```

安装库之后进入设置界面 `sudo raspi-config` 设置 OpenGL 驱动

