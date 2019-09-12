---
title: ubuntu部署ss过程中遇到的坑
date: 2019-09-12 11:26:25
tags: [ubuntu, linux, shadowsocks]
---

## 安装及配置ss

`pip install shadowsocks`

然后在顺手的位置创建一个配置文件，比如我放在`/etc`目录下，命名为`shadowsock.json`

编辑这个文件

```bash
{
    "server":"服务器 IP 或是域名",
    "server_port":端口号,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"密码",
    "timeout":300,
    "method":"加密方式"
}
```

<!-- more -->

保存后启动服务，这里会遇到第一个坑，就是sslocal这个程序安装后并没有添加到系统路径，会提示找到不到这个命令，可以用`whereis sslocal` 先找到这个在哪里，比如`/home/harold/.local/bin/sslocal`，再开启服务

`sudo /home/harold/.local/bin/sslocal -c /etc/shadowsocks.json -d start`

这种方式是设置后台运行，关闭命令行窗口也不会停止，停止把`start`换成`stop`即可，如果修改了配置，需要重启才会生效，同样的，关键字换成`restart`

### 保存为脚本自动运行

可以把命令行写到一个`.sh`文件中，放在桌面

```bash
#! /bin/bash
sudo /home/harold/.local/bin/sslocal -c /etc/shadowsocks.json -d start
```



## Chrome安装SwitchOmega遇到的坑

shadowsocks只是socks代理，转换成http，https代理在浏览器上需要配合SwitchOmega，火狐由于还没被墙，可以顺利安装并使用，但chrome被墙，就需要手动安装，新版chrome都不支持拖动crx文件安装扩展了，安装步骤如下

1. 打开扩展中心，打开右上角的开发者模式
2. 把下载好的crx文件改后缀名为`.zip`或者`.rar`，解压
3. 点击扩展中心左上角的`加载已解压的扩展程序`，选择解压后的文件夹
4. 如果提示安装失败，可以尝试将文件夹中`_metadata`修改为`metadata`

PS: 网上提到的一个转换软件`provixy`折腾了半天发现对我无效，不知道什么原因。