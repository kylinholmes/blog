---
title: cpp template 
tag: cpp
thumbnail: https://pic.kylinn.cloud/uploads/big/3ce124f97e406b8df21643d57ec4223f.jpg
---

## 模板判断类型是否相同：
```cpp
#include <type_traits>
bool res = std::is_same<T1, T2>::value;
```
Usage:
```cpp
std::is_same<int, int>::value;   //true
```
但是这个模板，非常严格。
对于类型T有：
```cpp
std::is_same<T, const T>::value;    //false
std::is_same<T,  T&>::value;        //false
std::is_same<T, const T&>::value;   //false
```
我们大部分时候对于以上这些类型并不想严格区分，需要用到`std::decay`，他可以去掉引用，const，退化成一般类型

cppref的栗子：
```cpp
#include <iostream>
#include <type_traits>

template <typename T, typename U>
struct decay_equiv : 
    std::is_same<typename std::decay<T>::type, U>::type 
{};

int main()
{
    std::cout << std::boolalpha
    << decay_equiv<int, int>::value << '\n'
    << decay_equiv<int&, int>::value << '\n'
    << decay_equiv<int&&, int>::value << '\n'
    << decay_equiv<const int&, int>::value << '\n'
    << decay_equiv<int[2], int*>::value << '\n'
    << decay_equiv<int(int), int(*)(int)>::value << '\n';
}
// 以上结果都为true
```