---
title: POJ 2105 IP Address
tag: [算法, C++, POJ]
date: 2021/04/08
---

### IP Address

|Time Limit: 1000MS	|	Memory Limit: 30000K|
|--|--|

**Description**
Suppose you are reading byte streams from any device, representing IP addresses. Your task is to convert a 32 characters long sequence of '1s' and '0s' (bits) to a dotted decimal format. A dotted decimal format for an IP address is form by grouping 8 bits at a time and converting the binary representation to decimal representation. Any 8 bits is a valid part of an IP address. To convert binary numbers to decimal numbers remember that both are positional numerical systems, where the first 8 positions of the binary systems are:

27   26  25  24  23   22  21  20 

128 64  32  16  8   4   2   1 


**Input**
The input will have a number N (1<=N<=9) in its first line representing the number of streams to convert. N lines will follow.

**Output**
The output must have N lines with a doted decimal IP address. A dotted decimal IP address is formed by grouping 8 bit at the time and converting the binary representation to decimal representation.

**Sample Input**

4
00000000000000000000000000000000 
00000011100000001111111111111111 
11001011100001001110010110000000 
01010000000100000000000000000001 

**Sample Output**

0.0.0.0
3.128.255.255
203.132.229.128
80.16.0.1

**Source**
México and Central America 2004
———————————————————————————————————————————————————————

### 题意：

这个题很简单，对应的2进制数转换成十进制数就行。
每8位是一个十进制数，相邻的两个数之间加上点。
```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <vector>
#include <cmath>
using namespace std;
#define  ll  long long

int n;
int temp;
int x;
int main(){
    scanf("%d",&n);
    while(n--){
        
        for(int i=1;i<=4;i++){
            temp = 0;
            for(int j=1;j<=8;j++){
                scanf("%1d",&x);
                temp += (x<<(8-j));
            }
            printf("%d",temp);
            if(i<=3)printf(".");
        }

        printf("\n");
    }
    return 0;
}
```
