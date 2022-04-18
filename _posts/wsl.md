---
title: wsl的安装及配置
tag: [杂技, Windows]
thumbnail: https://docs.microsoft.com/en-us/windows/wsl/media/terminal.png
date: 2021/5/7
---
# WSL安装以及配置
**WSL** 是 Windows Subsystem Linux 的缩写，就是Windows下的Linux子系统

如果你恰好有以下困扰
- 安装虚拟机太麻烦
- 虚拟机太大
-  不需要GUI(图形界面)
- 镜像下载太慢

那么使用WSL可能会更加方便：
- 简单的安装过程
- 几百兆的体积，不需要额外安装虚拟机
- 麻雀虽小，五脏俱全，如果有需要你甚至可以自己安装GUI

### WSL的安装
**1. 启用Windows功能**
Windows + S 搜索并打开“启用或关闭Windows功能”，勾选“适用于Linux的Windows子系统”项。
只有开启这项设置才能正常安装WSL。

**2.下载安装系统**
⚠️：注意不要去系统官网下载镜像文件，微软商店里提供的和官方的不一样。

要在 **微软商店** 里搜索wsl，个人感觉下载速度还是比较好的，如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505114103343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)
选择你自己需要的系统。

这里我下载了Ubuntu 18.04LTS，其实还有很多比如CentOS。
把这个装上，就算是安装完了

~~有些老师教学使用的是CentOS，其实平时使用起来是没什么差别的，不用专门下CentOS，Ubuntu也差不多嘛。~~ 

### 初始化
第一次打开以后会设置用户名和密码，注意你的密码不可见。
到此，WSL就算是安装完成并且**初始化成功**。

**如果**你需要进一步配置，可以继续往下看
@[TOC](全文目录)
### WSL的配置
#### 使用一个方便的文本编辑器
方便日后敲代码，vi有点不方便
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505114339435.png)


安装nano命令
```bash
sudo apt-get install nano
```

#### 换源
下载软件速度更加快

可以参考下文的图片

```bash
sudo nano /etc/apt/sources.list
```
```bash
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse 
```

可以用`#`把原来的注释掉
`Crtl + o 保存 Ctrl + x 退出`

**改成这个样子：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050511441692.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)


**更新刚刚的配置：** 
```bash
sudo apt-get update 
```

**更新一下软件：**
```bash
sudo apt-get upgrade 
```
#### 安装中文字体及设置： 
1、安装中文包： 

```bash
sudo apt-get install language-pack-zh-hans 
sudo apt-get install -y fonts-wqy-zenhei 
```

或者 

```bash
sudo apt install -y fonts-wqy-microhei 
```
2、打开 .profile 文件 

 

```bash
nano .profile 
```

 

在文本最后添加以下内容： 

```bash
export LANG="zh_CN.UTF-8"  
export LC_ALL="zh_CN.UTF-8" 
```

如下图： 
![在这里插入图片描述](https://img-blog.csdnimg.cn/202005051152561.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)
输入执行： 

```bash
sudo dpkg-reconfigure locales 
# 空格选择zh_CN.UTF-8 tab切换到确认 这里是拼音排序，所以z在最下面的位置
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507133555584.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2t5bGluaG9sbWVz,size_16,color_FFFFFF,t_70)
```
之后会让你选择默认的语言，选择 zh_CN.UTF-8 即可，就不放图了
```

然后
```bash
locale 
```
可以确定系统语言已经是中文 

## 重启你的WSL以后，配置完成 
**注意：** 仅仅关闭会话窗口是不能关闭WSL的。

在cmd里输入以下内容以用于关闭wsl(需要以管理员身份运行)
```bash
net stop LxssManager
```



cmd里输入`bash`也可以进入WSL

**相关文章**

- [WSL的图形化](https://blog.csdn.net/kylinholmes/article/details/105969403)(~~还没有开始更新...~~ wsl2支持了图形界面，弃坑)
- [linux里常用的软件](https://blog.csdn.net/kylinholmes/article/details/105570000)(还在更新)
- [Linux的目录介绍](https://blog.csdn.net/kylinholmes/article/details/106044138)

如果有疑问或者催更的，可以留言告诉我。