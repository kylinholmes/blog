---
title: Bytelib
tag: 杂技
---


最开始想的是，利用`void*`得到一个可以偏移任意字节数的指针，比如通过`p++`这样的操作，可以偏移到下7个、11个地址

```cpp
template<int step>
struct Byte{
    unsigned char byte[T];
};
```
这样就可以得到一个T个字节大小的类型，每次`p++`都可以偏移T个字节

后面想来想去觉得不对，改到最后，封装成了一个对象。
- 构造函数要求传入一个void*的指针p
- 用一个uchar的指针iter保存p
- 重载[]运算符，访问到从iter开始的第i个字节
- 重载ostream输出，4字节一个空格，一行8字节，地址从低到高输出


```cpp
template<size_t len>
struct Byte{
    unsigned char *iter;
    Byte() = delete;
    Byte(void* p):iter((unsigned char*)p){};
    unsigned char& operator[](size_t index){
        return *(iter + (index) % len);
    }
    friend ostream& operator<<(ostream &os, Byte<len> &b) {
        os << len << " Byte: ";
        for (int i=0; i < len ;i++){
            if(!(i % 8)) os << "\n"; else if(!(i % 4)) os << " ";
            os << int(b[i]) << ",";
        }
        return os;
    }
};

int main(){
    vector<int> a = {1,2,3,4,5,6,7};
    Byte<sizeof(a)>  tt =  &a;
    cout << tt << endl;
    
    return 0;
}
```