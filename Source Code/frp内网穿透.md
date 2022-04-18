---
title: frp内网穿透
tag: [杂技, Windows]
thumbnail: https://pic.kylinn.cloud/uploads/big/9e2a286381ba21086efab7495978c88f.png
---

## 安装和基本配置
利用[frp](https://github.com/fatedier/frp/blob/dev/README_zh.md)这个工具

下载解压以后是这些东西：
![](https://pic.kylinn.cloud/uploads/big/7a76bd42a67578138c1ae0d3811afaef.png)

其中：

`frps`和`frps.ini`是 **服务端的程序和配置文件**

`frpc`和`frps.ini`是 **客户端的程序和配置文件**

具体配置文件可以参考[文档](https://gofrp.org/docs/examples/)

## Linux 添加systemd
我的服务端是 `linux`

1. 将`systemd`中的`frps.service`拷贝到`/etc/systemd/system`路径下
2. 把`frps`和`frps.ini`分别拷贝到`/usr/bin/frps` 、`/etc/frp/frps.ini`，也可以修改service文件来改变位置
3. 打开frp服务端 `systemctl start frps`
4. 添加开机启动`systemctl enable frps`

## Windows 添加Service.msc
这里要重新下一个**windows版**的frp哦

先找个好位置放好，比如`C:\Frpc`


~~创建新服务，可以参考微软[官方文档](https://docs.microsoft.com/zh-cn/powershell/module/microsoft.powershell.management/new-service)~~

<font color=red>但是!! </font>这里不能用这个来添加服务，我也不知道为啥，反正一直报找不到指定文件

现在的解决办法参考了 [这里](https://github.com/fatedier/frp/pull/1904/commits/201733440d5b52516445d3731747ffb152e538b3)

![](https://pic.kylinn.cloud/uploads/big/04550da26e860763efb50b6b8c43aa31.png)
1. 首先需要一个[winsw](https://github.com/winsw/winsw/releases)，我把他重名成了上面的`frpc-service.exe`
2. 然后改一下`frpx-service.xml`的配置，如果放在了`C:\Frpc`就不用改了
3. 打开`terminal`，输入以下命令来安装服务
```powershell 
cd C:\Frpc # 切换到这个路径
./frpc-service.exe install # 执行安装命令
```

然后就 Over了！
另外卸载是这样的：

```powershell
./frpc-service.exe uninstall # 卸载命令
```