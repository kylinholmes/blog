---
title: Windows 配置
tag: 杂技
thumbnail: https://pic.kylinn.cloud/uploads/big/fd008d80a77ffae9f36a96272d64ba75.png
---

## 安装一些基本软件

1. **Terminal** ，好看的终端；[github地址](https://github.com/microsoft/terminal)，找到对应的Release，下载、安装
2. **PowerShell Core**； [github地址](https://github.com/Powershell/Powershell)，找到对应的Release，下载、安装
3. **Scoop**， Windows包管理器；打开`terminal`，选择刚刚装上的`pwsh`

## Scoop
`Scoop`和由它管理的程序，默认安装到`C:\Users\<user>\scoop\`，安装前通过设置环境变量改变默认安装位置
### 安装scoop
假设安装到`D:\Scoop`目录下
```powershell
[System.Environment]::SetEnvironmentVariable("Scoop","D:\Scoop")
```

安装时，需要网络通畅，如果有梯子的话，可以设置pwsh的代理可以加速下载安装：
比如我的V2rayN开启后，在最下面可以看到，socks5代理端口在10808，于是可以这样设置
```powreshell
$env:ALL_PROXY="socks5://127.0.0.1:10808"
# 或者用http协议也可以，不过要注意改协议和端口号
```

安装scoop:
````powershell
iwr -useb get.scoop.sh | iex
````

### 其他仓库

`Scoop`有很多仓库，其中`main`和`extra`比较常用，通过以下命令添加`extra`仓库

```powershell
scoop bucket add extra
```

~~`bucket`在scoop里就是`Repository`~~

![](C:\Users\Kylin\AppData\Roaming\Typora\typora-user-images\image-20210912005411790.png)

### 安装一些常用的程序

```powershell
scoop install 7zip aria2 bat git grep jetbrains-toolbox neofetch neovim sudo
```

除了这些，还有比如`python、go、gcc、llvm(clang)、java、php、nodejs cmake make`可以安装

[`Scoop`文档](https://github.com/lukesampson/scoop)

## Powershell 配置

### 安装`Oh-My-Posh`

```powershell
sudo Install-Module oh-my-posh -Scope CurrentUser
```
列出主题：`Get-PoshThemes`，修改`$PROFILE`文件，设置你的主题，重启`Shell`
[`Oh-My-Posh`文档](https://ohmyposh.dev/docs)
[`PowerShell`文档](https://docs.microsoft.com/zh-cn/powershell)

编辑`Powershell`的配置文件`$PROFILE`
[可以参考的配置文件](https://github.com/kylinholmes/pwsh_profile)



## Terminal 美化

`ctrl+,` 打开设置，修改`json`文件

`profiles->list-> <Shell>`存的是`Shell`的配置，根据`name`字段，找到对应的`Shell`，通过增加、修改来设置属性

### 设置透明属性

```json
"useAcrylic": true, 		// 开启透明效果
"acrylicOpacity": 0.75,		// 透明度
```

### 设置字体

```json
"fontFace": "JetBrainsMono Nerd Font",
```
这个字体需要额外下载，在`Scoop`的`nerd-font`仓库，可以下载

### 设置主题

主题要存在于这个`json`的`schemes`里，自带的`Half Dark`比较合适，不喜欢也可以自己倒腾

```json
"colorScheme": "One Half Dark",
```

### 设置背景

```json
"backgroundImage": "C:\\Users\\<user>\\Pictures\\xxx.jpg",
"backgroundImageOpacity": 0.3,
```

[`Terminal`文档](https://docs.microsoft.com/zh-cn/windows/terminal/get-started)

## WSL

具体配置方法，可以参考先前的[文章](https://kylinn.cloud/2021/05/03/wsl)，也可以用`Arch`，记得升级到`wsl2`

[WSL文档](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10)



