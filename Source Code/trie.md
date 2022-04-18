---
title: 来 看 T r i e 吧
tag: [算法, 字典树, C++, 数据结构]
date: 2021/04/08
---
**Trie** 念做 try，就是字典树，也叫前缀树

是一种主要用于字符串快速检索的多叉树结构

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ia2ltZy5jZG4uYmNlYm9zLmNvbS9waWMvZDYyYTYwNTkyNTJkZDQyYTc0NWNjMmMyMDMzYjViYjVjOWVhYjgwNg?x-oss-process=image/format,png)
可以做什么呢，比如你输入了一大堆已有的字符串，可以很快判断一个新的给定的字符串是否在已有的字符串里出现过

```cpp
const SIZE = 1e4+5;
bool end[SIZE]
int tire[SIZE][26], tot = 1; //假设只有小写字母 

void insert(char s[]){
	int L = (int)strlen(s),p = 1;
	for(int k=0;k<L;k++){
		int ch = s[k] - 'a';
		if(tire[p][ch] == 0) trie[p][ch] = ++tot;	
		// tire[p][ch] == 0 表示没有出现过这个字符串
		// 对于一个确定的字符串前缀，有唯一对应的数字tot，若没有出现这样的前缀，那么++tot
		p = trie[p][ch];
	}
	end[p] = 1;//标记下这个字符串的结尾
}

bool search(char s[]){
	int L = (int)strlen(s),p=1;
	for(int k=0;k<L;k++){
		p = trie[p][s[k] - 'a'];
		if(p == 0) return false;	
	}
	return end[p];
}
```
### 相关解释
我觉得嘛，
首先， 数字 p 有对应的唯一字符串
那么，这个 `trie[p][ch]` 可以理解成：
以p为前缀的字符串，加上ch以后的对应的数字。

所以就很好理解了嘛
`insert`的时候，如果不存在这样的p，那么就立刻++tot，这时p就存在了。
`search`的时候，如果不存在这样的p，那么就是找不到，返回false。

这个字典树有什么用呢？
比如说，可以根据前缀预测出后面可能的字符，因为对于一个p来说，他可能的后缀是可以找到的。像什么 **搜索** 就可以通过这种方式建立索引。