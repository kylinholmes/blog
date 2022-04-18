---
title: 字符串算法
tag: Algorithm
thumbnail: https://pic.kylinn.cloud/uploads/big/de16926a0216ca852c56a8dc5d91284b.jpg
date: 2021/3/1
---

## Rope data structure
字符串拼接数据结构
本质上是一颗树，字符串的拼接过程，可以看成将两棵树，通过创建一个父节点，合并成一棵树的过程
叶节点可以是一个单词，这样split的时候，也会很好处理，自己感觉吧
> to be continue

## Sunday
字符串匹配算法,比kmp更高效、更好理解，时间复杂度最坏O(n)
可以参考 <a href="https://blog.csdn.net/q547550831/article/details/51860017">blog</a>

```cpp
// ref of Main string
// ref of Pattern string
// 256 is greater than unsigned char, it's only effective for ascii encoding
int Sunday(const ::std::string &Main, const ::std::string &Pattern, int Max = 256){
    // init
    int n = Main.size(), m = Pattern.size();
    int shift[Max];
    for (auto &i : shift) 
        i = m + 1;
    for (int i = 0; i < m; i++) 
        shift[Pattern[i]] = m - i;

    // matching
    for (int res = 0; res <= n - m; res += shift[Main[res + m]]){
        int j = 0;
        while (Main[res + j] == Pattern[j]){
            j++;
            if (j >= m)
                return res;
        }
    }
    return -1;
}

int main(){
    string a = "substring searching";
    string b = "search";
    cout << Sunday(a, b) << endl; // 10
}
```
