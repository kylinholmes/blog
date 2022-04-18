---
title: POJ 2063 投资 
tag: [算法, C++, 背包, POJ]
date: 2021/04/08
---
**Description**

John never knew he had a grand-uncle, until he received the notary's letter. He learned that his late grand-uncle had gathered a lot of money, somewhere in South-America, and that John was the only inheritor.
John did not need that much money for the moment. But he realized that it would be a good idea to store this capital in a safe place, and have it grow until he decided to retire. The bank convinced him that a certain kind of bond was interesting for him.
This kind of bond has a fixed value, and gives a fixed amount of yearly interest, payed to the owner at the end of each year. The bond has no fixed term. Bonds are available in different sizes. The larger ones usually give a better interest. Soon John realized that the optimal set of bonds to buy was not trivial to figure out. Moreover, after a few years his capital would have grown, and the schedule had to be re-evaluated.
Assume the following bonds are available:
| Value	|Annual interest|
|--|--|
| 4000 | 400 |
|3000|250|



With a capital of e10 000 one could buy two bonds of $4 000, giving a yearly interest of $800. Buying two bonds of $3 000, and one of $4 000 is a better idea, as it gives a yearly interest of $900. After two years the capital has grown to $11 800, and it makes sense to sell a $3 000 one and buy a $4 000 one, so the annual interest grows to $1 050. This is where this story grows unlikely: the bank does not charge for buying and selling bonds. Next year the total sum is $12 850, which allows for three times $4 000, giving a yearly interest of $1 200.
Here is your problem: given an amount to begin with, a number of years, and a set of bonds with their values and interests, find out how big the amount may grow in the given period, using the best schedule for buying and selling bonds.
**Input**

The first line contains a single positive integer N which is the number of test cases. The test cases follow.
The first line of a test case contains two positive integers: the amount to start with (at most $1 000 000), and the number of years the capital may grow (at most 40).
The following line contains a single number: the number d (1 <= d <= 10) of available bonds.
The next d lines each contain the description of a bond. The description of a bond consists of two positive integers: the value of the bond, and the yearly interest for that bond. **The value of a bond is always a multiple of $1 000.** The interest of a bond is never more than 10% of its value.
**Output**

For each test case, output – on a separate line – the capital at the end of the period, after an optimal schedule of buying and selling.
**Sample Input**

1
10000 4
2
4000 400
3000 250
**Sample Output**

14050
**Source**

Northwestern Europe 2004

这个题读懂以后就应该很容易想到完全背包吧。没什么难点
注意上面加粗的文本：
> **The value of a bond is always a multiple of $1 000.**

最开始我空间没开够(1e5+5)然后读题发现范围到了1e7，后来想到数据好像都是有个k倍，去找了一下还真是1000倍，然后处理一下就好了。
```cpp
//
//  main.cpp
//  Problem
//
//  Copyright © 2020 Kylin. All rights reserved.

#include <iostream>
#include <fstream>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <cstring>
#include <string>
#include <bitset>
#include <set>
/*
#include <unistd.h>     //包含<unistd.h>
#include <sys/types.h>  //包含<sys/types.h>
 */

#pragma GCC optimize("Ofast")

using namespace std;
#define ll  long long
#define lowbit(x) (x)&(-x)
#define print_str(a) do{for(int i=0;i<strlen(a);i++)printf("%c",a[i]);printf("\n");}while(0)
#define ms(a,b) memset(a,b,sizeof a)
#define INF 0x3f3f3f3f

const int N = 1e6+5;
int t,n;
int v[11],w[11];
int f[N];
int captial,year;
int main()
{
    scanf("%d",&t);
    while(t--){
        scanf("%d%d%d",&captial,&year,&n);
        for(int i=1;i <= n;i++){
            scanf("%d%d", v+i, w+i);
            v[i] /= 1000;						//	在这里处理一下
        }
        ms(f,0);
        while(year--){
            int temp = captial/1000;			//	对应的这里处理一下
            for(int i = 1;i <= n; i++)
                for(int j = v[i];j <= temp; j++)
                    f[j] = max(f[j], f[j - v[i]] + w[i]);
            captial += f[temp];					//	结果加到 captial 上
        }
        printf("%d\n",captial);
    }
    return 0;
}


```
