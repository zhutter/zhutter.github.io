---
title: hexo + next 的部署
date: 2019-08-08 16:25:09
tags: [Hexo, NexT]
---

# Hexo博客框架+NexT主题

## 1.安装Hexo

在电脑上已经安装好Node.js(version >= 6.9) 和 Git 后, 只需输入

`npm install -g hexo-cli` 即可快速安装

如果电脑中没有上述两个程序, 请依照[官网](https://hexo.io/zh-cn/docs/)文档指示安装

安装好后, 在想要的任意位置建立一个文件夹用来存放Hexo的源文件, 如个人新建了`E:\hexo`这个文件, 接着输入以下命令

```bash
hexo init E:\hexo
cd E:\hexo
npm install
```

其他未尽事宜参考官网, 可以使用

```bash
hexo clean
hexo g
hexo s
```

来预览

## 2.安装NexT

打开Hexo的安装文件夹, 如 `E:\hexo`, 在Git bash中输入

`git clone https://github.com/iissnan/hexo-theme-next themes/next`

然后在_config.yml中, 找到`theme` 字段, 将其值更改为next

`theme: next`

这样就安装完成了,  可以使用与上述预览相同代码来预览主题是否生效

未尽事宜, 参考NexT[官网](https://theme-next.iissnan.com/getting-started.html)

