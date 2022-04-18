---
title: C++递归过程中出现的问题
tag: C++
date: 2021/04/08
---

## 提出问题
一个蛮有意思的问题，朋友问我的。
先看遇到问题的代码
```cpp
#include<iostream>
using namespace std;

int a[5] = {1,2,3,4,5};
int f(int i){
	if(i < 5) return a[i]+f(i+1);
}
int main(){
	cout << f(0) << endl;
        return 0;
}
```
很明显这里的 f( ) 有问题，因为 i == 5的时候没有返回值
- 如果是`clang`这里会直接报错。

- `gcc`编译会因为`<iostream>`报错

```bash
/tmp/ccv3ma76.o：在函数‘main’中：
a.cpp:(.text+0x47)：对‘std::cout’未定义的引用
a.cpp:(.text+0x4c)：对‘std::ostream::operator<<(int)’未定义的引用
a.cpp:(.text+0x51)：对‘std::basic_ostream<char, std::char_traits<char> >& std::endl<char, std::char_traits<char> >(std::basic_ostream<char, std::char_traits<char> >&)’未定义的引用
a.cpp:(.text+0x59)：对‘std::ostream::operator<<(std::ostream& (*)(std::ostream&))’未定义的引用
/tmp/ccv3ma76.o：在函数‘__static_initialization_and_destruction_0(int, int)’中：
a.cpp:(.text+0x87)：对‘std::ios_base::Init::Init()’未定义的引用
a.cpp:(.text+0x96)：对‘std::ios_base::Init::~Init()’未定义的引用
```
注释掉相关代码以后还是会报错，也就是说只要include这个头文件就会报错
```bash
/tmp/ccs8zhVg.o：在函数‘__static_initialization_and_destruction_0(int, int)’中：
a.cpp:(.text+0x7f)：对‘std::ios_base::Init::Init()’未定义的引用
a.cpp:(.text+0x8e)：对‘std::ios_base::Init::~Init()’未定义的引用
```
删除`iostream`以后，改用`cstdio`的printf可以正常编译
**找到报错原因了**，主要是因为gcc不会自动链接STL标准库，加上参数`-lstdc++`可以正常编译，详细解释可以看这篇[博客](https://blog.csdn.net/qq_28114615/article/details/86663967)。

- `g++`可以直接成功编译，没有任何问题。

在gcc和g++编译以后都可以运行。
## 发现问题：
运行结果是20，而不是15。
## 作出假设
- 可能是dev自己给f最后加了一句话
```cpp
return i;
```
- dev坏了（ @ _ @ ）
## 解决方法

先查看相关的的汇编码：

```bash
_Z1fi:
.LFB0:
      	.cfi_startproc
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        pushq   %rbx
        subq    $24, %rsp
        .cfi_offset 3, -24
        movl    %edi, -20(%rbp)
        cmpl    $4, -20(%rbp) 	# 猜测是if对应的判断
        jg	.L2 				# 大于跳转跳转到L2 
        # 其实我觉得这里应该是jge才对，因为jge是大于等于，jg是大于跳转 jump if greater 
        # 而且jg不是要判断两个数的哇，怪我确实不会汇编 [ q A q] ~~
        movl    -20(%rbp), %eax
        cltq
		movl    a(,%rax,4), %ebx
        movl    -20(%rbp), %eax
        addl    $1, %eax
        movl    %eax, %edi
        call    _Z1fi			# 调用自身
        addl    %ebx, %eax
        jmp     .L1 			# jmp无条件跳转
.L2:							# 注意这里是空的
.L1:
    	addq    $24, %rsp
        popq    %rbx
        popq    %rbp
        .cfi_def_cfa 7, 8
        ret
	.cfi_endproc
```
修改f( )以后

```cpp
int f(int i){
	if(i < 5) return a[i]+f(i+1);
	return 0;
}
```
对应汇编码
```bash
		jg	.L2
        movl    -20(%rbp), %eax
        cltq
		movl    a(,%rax,4), %ebx
        movl    -20(%rbp), %eax
        addl    $1, %eax
        movl    %eax, %edi
        call    _Z1fi
        addl    %ebx, %eax
        jmp     .L3
.L2:
    	movl    $0, %eax
.L3:
    	addq    $24, %rsp
        popq    %rbx
        popq    %rbp
```
可以很明显的发现 .L2这里多了东西，所以我猜测：

.L2就是对应 if 后面多加的 return，他会把0放到 `eax` 寄存器里。

`eax`是一个累加器，因为上一次递归在运行的最后，寄存器里放的是a[4] ~~也就是5~~ ，所以累加器里还是5。如果不把0放到`eax`，那么他就把现有的5再加一次，所以结果就是15 + 5;

```cpp
正确的函数展开
a[0] + (a[1] + (a[2] + (a[3] + (a[4] + (0)))))
错误的函数展开
a[0] + (a[1] + (a[2] + (a[3] + (a[4] + (?)))))
因为这里的问号，没有修改过值，所以eax里是上一次的值，也就是a[4]
这里的一对括号相当于一次函数递归
```

同样的，如果我们把结束条件i < 5 改成 i < 4 结果就变成了14，而不是10；

## 总结
所以这个问题就是这样的。老铁们我做的对吗？~~此处应有正道的光~~ 