---
title: windows 制作macOS镜像然后安装
tag: [杂技, Windows]
thumbnail: https://pic.kylinn.cloud/uploads/big/f117dd8066d9ba124efc503eb00c5fb7.jpg
---
# Windows 下 MacOS 10.14 mojave 的 重装
[TOC]
## 前言
因为 **Catalina** 下 Steam 里有 **相当一部分** 游戏不能正常运行，所以推荐 **Mojave**
**！！本篇教程无关 Hackintosh** ，确认你有mac电脑以后阅读。
**主要流程参考目录即可**
![图片来自互联网](https://img-blog.csdnimg.cn/20200503180740146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)
## 镜像文件下载
首先需要一个最基本的文件就是Mojave的镜像文件

~~这里附上官网 mojave [下载链接](https://support.apple.com/kb/DL1981?viewlocale=zh_CN&locale=zh_CN)~~
~~经过一晚上的折腾，发现这个不是原版镜像，只是mojave的升级包。~~ 

这里附上  **带usb引导的镜像**  

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505012913680.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)

[感谢这个老哥 18024****82@189.cn 的分享](https://www.misonsky.cn/145.html#%E9%95%9C%E5%83%8F%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80)
下的时候可以一个一个下，不要多选了下
下载完成以后是4个rar的part文件，解压出来得到一个文件

- macOS Mojave 10.14.6【18G84】原版带Clover引导和PE镜像.dmg

这里下载好之后，可以对下载的文件进行一次检验
用 **Hasher** 这个软件对那4个part文件检查，是否有错误


## 启动盘的制作



我们直接用 [**balenaEtcher**](https://www.balena.io/etcher/) 烧录这个镜像文件到u盘即可。
只需**以下三步**，就可以完成 Windows下 启动盘的制作 ：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly93d3cuYmFsZW5hLmlvL3N0YXRpYy9zdGVwcy04MDA2ZGNhNTczMjM3NTZiMWI4NGZiOTQwODc0MjQwOS5naWY#pic_center)

选择刚刚下载的镜像文件(.dmg)，选择你的U盘，然后就可以 **Flash！**
之后等待烧录结束。
	
## 安装Mojave

1. 将烧录好的u盘插到你的mac上
2. 按下开机键
3. 随后马上按住option键

等待屏幕亮起来可以看到 **install mojave** 这个分区。
~~可能有什么EFI分区，Clover分区，无视即可~~ 

稍加等待后
### 硬盘分区
先对你的硬盘分区，如果已经分好区了就可以忽略这条。
分区按自己喜欢的大小来就好。

容易出现的第一个问题：
![在这里插入图片描述 多打点字，](https://img-blog.csdnimg.cn/20200505010215388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)
这里默认 选GUID分区
- GUID是Intel芯片
- 主引导记录是给Windows用的
- apple分区是早期的powerPC芯片

容易出现的第二个问题：
[分区格式](https://support.apple.com/zh-cn/HT208018)
尽量选APFS格式的，macos日志是老分区格式了，据说APFS对固态有迷之加速

到这里 **默认** 各位已经分好区了

### 系统的安装
其实这里没什么需要说的了

提一下如果出现了 **提示应用程序副本已损坏** 法这类情况
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050501234185.png)


在保证断网的情况下，打开终端
![图片描述](https://img-blog.csdnimg.cn/20200505011005114.png)
输入以下命令
4个12 + 2015
```bash
date 121212122015
```


然后就可以进行安装了。
之后设置好地区，个人喜好，系统就算安装完成。

如果觉得有帮助到你的话，可以点一下赞，给我一个反馈。