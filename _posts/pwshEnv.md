---
title: Windows 设置环境变量
thumbnail: https://pic.kylinn.cloud/uploads/big/128e028306976ccfae09d1d322a6cada.jpg
date: 2021/11/24
---

# 因为渲染问题，有些代码不能正确显示，我把它放在[csdn](https://blog.csdn.net/kylinholmes/article/details/120195414)上了
如果有问题，参考csdn和github

## 环境变量是什么
1. 环境变量是一种在系统里的变量，可以理解成一种属性，就放在那，有需要的程序就会去读，类似写代码里的全局变量
2. 通常用作，程序运行时的一些参数
3. 环境变量分为**用户**，**系统**。


举个经典的栗子，Java安装的时候，需要自己手动配置环境变量，非常头大
但其实Windows可以通过命令行一句话设置。
- 假设我们需要设置`JAVA_HOME`这个环境变量

## PowerShell 中的Env
在powershell里有3个环境变量，除开上面说的**用户**和**系统**，还有一个**临时环境变量**~~(自己取的名字)~~，就是`env:`
- 优先级：**临时**>**用户**>**系统**
- 彼此不会相互覆盖

### 临时环境变量的位置
环境变量放在`env:`里面，这块变量区域被映射成了一个文件分区
就像`C:` `D:` `E:` `F:` 一样
可以用进入
```powershell
cd env:
```
### 临时环境变量：
```powershell
$env:[variable name] = 'value'
```
`example:`
```powershell
$env:JAVA_HOME="C:\JAVA"
```
![](https://img-blog.csdnimg.cn/d1817024df3541fb8e94ed7df84aad41.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAa3lsaW5ob2xtZXM=,size_20,color_FFFFFF,t_70,g_se,x_16)

当你退出当前终端后，临时环境变量就会失效，所以我们通常设置永久的

## 永久环境变量
就像上面说的，永久的还分为，**用户**和**系统**
```powershell
[Environment]::SetEnvironmentVariable("[variable name]","[value]","<User | Machine>")
```
`Example:`
第三个参数可写可不写，默认是`User`
```powershell
[Environment]::SetEnvironmentVariable("JAVA_HOME","D:\JAVA","Machine")
```
下面这个就**是**永久修改的：
不过可能需要重启电脑

![](https://img-blog.csdnimg.cn/1273928480ab477784218d8f621f8913.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAa3lsaW5ob2xtZXM=,size_20,color_FFFFFF,t_70,g_se,x_16)



## 删除环境变量
- 当`[value]`为`$null`即可删除环境变量

`example:`
```powershell
$env:JAVA_HOME=$null
```
```powershell
[Environment]::SetEnvironmentVariable("JAVA_HOME",$null)
```

## 往`PATH`添加一条环境变量
**注意：**
因为path里每一条记录中间用`;`分开，所以你在加入一条记录的时候，需要用`;`作为前缀
（`Unix-like`分割符是`:`）
```powershell
$JAVA_HOME = "E:\JAVA"
$env:PATH += ";"+$JAVA_HOME
```
当然这样就是暂时的，全局永久的方法如下：
```powershell
$oldpath = [Environment]::GetEnvironmentVariable('PATH', 'Machine')
$newpath = $oldpath + ';New Value'
[Environment]::SetEnvironmentVariable("PATH", $newpath, 'Machine')
```
### 关于`PATH`这个变量
`PATH`的用处，通常用于记录一些可执行文件的位置，
比如`PATH`里有一条变量是 `C:\Program Files\java\bin`
那么，你在打命令`java`的时候，就会去这个目录下面找这个可执行文件
其等效于：
`C:\Program Files\java\bin\java.exe`
如此，就可以在 `powershell` 的任何位置，运行一个`java.exe`，而不用指明其完整路径。

所以，所谓的配置Java 的环境变量，就是在`PATH`里加上`java.exe`的所在路径，以便我们可以方便的使用`java.exe`

## powershell脚本
自己封装了一下，把这段脚本加到`$PROFILE`里，就可以用了。路径会添加到用户所在的`PATH`里面

不添加到系统是避免系统环境变量损坏导致出现奇怪bug。

因为`$`符号在渲染的时候起了冲突，我把代码放到[github](https://github.com/kylinholmes/pwsh_profile)上了
```powershell
New-Alias ade   Add-UserEnvironmentVariable
function Add-UserEnvironmentVariable($NewPath){
        $PreviousPath = [System.Environment]::GetEnvironmentVariable("Path", "User")
        $New = "$PreviousPath;$NewPath"
        [System.Environment]::SetEnvironmentVariable("Path", "$New", "User")
        return New-Object psobject -Property @{Path = $New -split ";"}
}
```
Example:
```powershell
ade 'D:\JAVA HOME\bin'
```



## 相关参考：

[微软官方文档](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1)

[Windows Forums](https://www.tenforums.com/tutorials/121797-delete-user-system-environment-variables-windows.html)
