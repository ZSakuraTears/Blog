---
title: 'Linux(deepin)日常操作'
date: 2020-11-29 17:53:09
tags: [Linux]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/r7zm17%20(1).jpg
isTop: true
---
记录日常使用linux一些操作
deepin永远滴神！！！
<!-- more -->
### 安装deb文件
在deb文件目录下终端输入`sudo apt-get xx.deb`(xx为文件名)
### 打开tag.gz文件
情况一(没有可执行文件)：解压缩后终端进入文件目录，然后cd进入/bin，执行./xxx.sh(xxx为程序名)
情况二(有可执行文件)：直接运行可执行文件即可运行
### 进入root身份
终端输入`su`然后输入密码(开机密码)
如果提示su鉴定故障可以输入`sudo su`

### 双系统切换时间问题

终端输入`timedatectl set-local-rtc 1`

### 双系统开机默认linux更改
1.ctrl+alt+T打开终端，输入`sudo gedit /etc/default/grub`
2.验证密码，grub配置文件被打开
3.将弹出的文件中文本“GRUB-DEFAULT=0”中的0修改为2.（我这里是2，具体数字应该和选择系统的时候win系统的位置-1相同。注意这个-1，因为它是从上到下从0开始排序，所以我这里win系统是第三位，就改成2）
4.保存文件。←这时可能会弹出警告框，但是一般情况下好像并没有什么关系
5.在终端输入`sudo update-grub`以更新配置
6.重启即可发现已经修改完毕

### linux显示系统信息
终端执行`sudo apt-get install screenfetch`安装screenfetch
然后执行`screenfetch -s`显示系统信息

### BIOS声音问题
(deepin)有时候发生错误(比如在QQ输入框没有字的情况下按退格),会出现“嘟”的一声。这是主板BIOS声音没关的问题。
执行 ``sudo dedit /etc/modprobe.d/alsa-base-blacklist.conf``，输入
```
blacklist pcspkr
blacklist snd_pcsp
```
保存后执行 ``sudo update-initramfs -u ``后重启即可。
