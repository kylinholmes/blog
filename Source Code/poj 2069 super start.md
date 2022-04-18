---
title: POJ 2069 Super Start
tag: [算法, C++, 退火, POJ]
date: 2021/04/08
---



[退火法](https://baike.baidu.com/item/%E6%A8%A1%E6%8B%9F%E9%80%80%E7%81%AB%E7%AE%97%E6%B3%95/355508?fromtitle=%E9%80%80%E7%81%AB%E7%AE%97%E6%B3%95&fromid=6081525&fr=aladdin)

主要参考这篇[文章](https://www.cnblogs.com/heisenberg-/p/6827790.html)

**Description**

During a voyage of the starship Hakodate-maru (see Problem 1406), researchers found strange synchronized movements of stars. Having heard these observations, Dr. Extreme proposed a theory of "super stars". Do not take this term as a description of actors or singers. It is a revolutionary theory in astronomy.
According to this theory, starts we are observing are not independent objects, but only small portions of larger objects called super stars. A super star is filled with invisible (or transparent) material, and only a number of points inside or on its surface shine. These points are observed as stars by us.

In order to verify this theory, Dr. Extreme wants to build motion equations of super stars and to compare the solutions of these equations with observed movements of stars. As the first step, he assumes that a super star is sphere-shaped, and has the smallest possible radius such that the sphere contains all given stars in or on it. This assumption makes it possible to estimate the volume of a super star, and thus its mass (the density of the invisible material is known).

You are asked to help Dr. Extreme by writing a program which, given the locations of a number of stars, finds the smallest sphere containing all of them in or on it. In this computation, you should ignore the sizes of stars. In other words, a star should be regarded as a point. You may assume the universe is a Euclidean space.
**Input**

The input consists of multiple data sets. Each data set is given in the following format.

n
x1 y1 z1
x2 y2 z2
. . .
xn yn zn

The first line of a data set contains an integer n, which is the number of points. It satisfies the condition 4 <= n <= 30.

The location of n points are given by three-dimensional orthogonal coordinates: (xi, yi, zi) (i = 1, ..., n). Three coordinates of a point appear in a line, separated by a space character. Each value is given by a decimal fraction, and is between 0.0 and 100.0 (both ends inclusive). Points are at least 0.01 distant from each other.

The end of the input is indicated by a line containing a zero.
**Output**

For each data set, the radius of the smallest sphere containing all given points should be printed, each in a separate line. The printed values should have 5 digits after the decimal point. They may not have an error greater than 0.00001.
**Sample Input**

4
10.00000 10.00000 10.00000
20.00000 10.00000 10.00000
20.00000 20.00000 10.00000
10.00000 20.00000 10.00000
4
10.00000 10.00000 10.00000
10.00000 50.00000 50.00000
50.00000 10.00000 50.00000
50.00000 50.00000 10.00000
0
**Sample Output**

7.07107
34.64102
**Source**

Japan 2001
题目的大概意思就是说，给你几个空间中的点，要找到最小 包含所有的点 的球体半径。
思路就是这么个思路：先找到最远的，然后慢慢变小，找到合适的点。
最开始我的思路是硬算，看了一下数据，30，能过。然后要去解方程，列算式，有点麻烦。这个思路类似[这样](https://wenku.baidu.com/view/82abe82ebd64783e09122b14.html)。
后来百度看了别人的算法。

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

const int N = 50;
const double eps = 1e-7;
int n;
struct P{
    double x,y,z;
}a[N],z;
double ans;

double dis(P a,P b)
{
    return sqrt((a.x-b.x)*(a.x-b.x)+(a.y-b.y)*(a.y-b.y)+(a.z-b.z)*(a.z-b.z));
}
void solve()
{
    double step=100,mt;
    z.x=z.y=z.z=0;
    int s=0;
    while(step>eps)
    {
        for(int i=0; i<n; i++)
            if(dis(z,a[s])<dis(z,a[i])) s=i;
        mt=dis(z,a[s]);
        ans=min(ans,mt);
        z.x+=(a[s].x-z.x)/mt*step;
        z.y+=(a[s].y-z.y)/mt*step;
        z.z+=(a[s].z-z.z)/mt*step;
        step*=0.98;
    }
}

int main(){
    while(scanf("%d",&n)&&n){
        ans = INF;
        for(int i=0;i<n;i++)scanf("%lf%lf%lf",&a[i].x,&a[i].y,&a[i].z);
        solve();
        printf("%.5lf\n",ans);
    }
   
    return 0;
}

```
