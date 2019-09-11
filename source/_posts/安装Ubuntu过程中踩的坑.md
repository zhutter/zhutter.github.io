---
title: '安装Ubuntu过程中踩的坑'
date: 2019-09-11 19:58:55
tags: [ubuntu, windows10, dual]
---

# 安装ubuntu过程中遇到的坑

## win10安装ubuntu需要做的预备工作

1. 需要把“快速启动”，“安全启动”关闭

快速启动：`ctrl+x` 找到“电源选项” --> ”选择电源按钮功能“ --> 把“启用快速启动”勾掉

安全启动：进入bios把“secure boot”字样设置成`disable`

2. `ctrl+x` 找到“磁盘管理“，选个剩余空间大的磁盘，右击选择”压缩卷“，分50G出来



## ubuntu安装程序启动一会就黑屏关机

在进入选择是试用还是安装的界面处，按`e`，然后在`quite splash` 代码后面添加`nomodeset`，即`quite splash nomodeset`，如果安装好后开机时出现类似的情况，做同样的处理

这样操作不能一劳永逸，安装好后，进入系统，打开终端

`sudo vi /etc/default/grub`

找到

`GRUB_CMDLINE_LINUX_DEFAULT=“quiet splash”`
修改为：
`GRUB_CMDLINE_LINUX_DEFAULT=“quiet splash nomodeset”`

然后更新grub

`sudo update-grub`



## nvida显卡驱动安装

没有网上说的那么麻烦，直接在“软件和更新”里找到对应的专用推荐驱动即可（显示tested字样）

## “Ubuntu 18.04.2 LTS _Bionic Beaver_ - Release amd64 (20190210)” 的盘片插入驱动器“/cdrom/”再按「回车」键

1. `cd /etc/apt`
2. `sudo vi sources.list`
3. 注释掉`deb cdrom`开头的行

## 用UltraISO时遇到的坑

一直提示u盘忙，怎么格式化，退软件，重启电脑都没用，后来用老毛桃还原了下u盘就可以了。。虽然不知道是什么原理，但是就是好了

还有个方法就是更改写入方式，改成可以写入的方式即可

## 安装后如何引导双系统

如果电脑不是efi模式，那么下载easyBCD可以轻松搞掂，网上也可以搜索到大量的教程

如果电脑是efi模式，就进bios把ubuntu启动引导第一位，就可以选择grub2引导

## ubuntu firefox字体模糊

由于ubuntu firefox字体模糊，需要安装这两种字体，安装完成后，字体模糊的问题得到解决 
`sudo apt-get install font-wqy-zenhei` 
`sudo apt-get install font-wqy-microhei`

设置完成后在firefox里面修改成对应的字体即可

## 没声音问题

```bash
sudo apt-get remove --purge alsa-base pulseaudio
sudo apt-get install alsa-base pulseaudio pavucontrol
sudo alsa force-reload
```

