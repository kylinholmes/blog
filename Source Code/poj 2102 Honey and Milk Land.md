---
title: POJ 2102 Honey and Milk Land
tag: [算法, C++, POJ]
date: 2021/04/08
---


### Honey and Milk Land
|Time Limit: 1000MS		|Memory Limit: 64000K|
|--|--|


**Description**
Bad rumors are spreading over the Land of Honey and Milk. Informed people say that the milk in the famous grid of milk rivers is turning sour. Of course, the security service quickly found out that the people are informed by the Kingdom of Tar, which is jealous to tourist popularity of the land. However, this discovery does not help to stop these rumors. The government wants to prevent crisis of the tourist industry, so it wants to establish daily monitoring of the rivers.
A new Milk Security Department is established, which is responsible for preventing the milk from turning sour. It's equipped with powerful boilers and pasteurizer, so any danger for the milk can be quickly neutralized. To better fight the new threat, the department needs to know about possible dangers beforehand. They have a helicopter, capable to check milk freshness. The equipment is perfect. It's enough just to cross a river in any place in order to detect all its potentially dangerous places.
To start the Milk Security Department operations, the government needs to add funding of the Service to the Land budget. One of the issues is the morning route of the helicopter. The helicopter should check all the rivers in the shortest time. They need to determine the price of this flight to add it to the budget.
The grid consists of two sets of milk rivers. Rivers from the first set run from North to South, rivers from the second set --- from East to West. The rivers are straight. The rivers from each set are parallel and the distance between the adjacent rivers is known. There are n rivers, running from North to South and e rivers, running from East to West.
The government needs to determine the minimal morning flight cost. Each kilometer costs 1 honey barrel, the Land national currency. The cost of take-off and landing is not included into this cost. You may freely choose the starting and ending points of the flight.

**Input**
The first line of the input file contains n and e (1 <= n, e <= 1 000). The second line contains n - 1 integer numbers that represent distances (in kilometers) between adjacent rivers running from North to South, listed from East to West. The third line contains e - 1 integer numbers that represent distances (also in kilometers) between adjacent rivers running from East to West, listed from North to South. The distance between any two adjacent rivers does not exceed 27 kilometers.

**Output**
Output the minimal morning flight cost in honey barrels. Since there is no smaller denomination, you must output the minimal integer number of honey barrels that would be sufficient to support the flight.

**Sample Input**

10 10
2 2 2 2 2 2 2 2 2
2 2 2 2 2 2 2 2 2

**Sample Output**

26

**Source**
Northeastern Europe 2004, Northern Subregion
———————————————————————————————————————————————————————
### 题意：
告诉你长宽，求对角线，向上取整。
给的数据是
第一行 从北到南的河流和从东到西的河流条数
第二行 N ->S 里河流的间隔
第三行 E->W 里的河流间隔
~~非常罗嗦的一道题，结果思路和白给的一样~~ 
```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <vector>
#include <cmath>
using namespace std;
#define  ll  long long

int n,e;
int s1,s2;
int temp;
int main(){
    scanf("%d%d",&n,&e);
    for(int i=1;i<n;i++){scanf("%d",&temp),s1+=temp;}
    for(int i=1;i<e;i++){scanf("%d",&temp),s2+=temp;}
    if(n==1&&e==1)printf("0\n");
    //else printf("%d\n",(int)ceil(sqrt(s1*s1+s2*s2)));
    else cout << (int)ceil(sqrt(s1*s1+s2*s2)) << endl;
    return 0;
}
```
这里提交用C++ 会报编译错误，如果是G++就不会有这个问题。
- **Compile Error**
Main.cpp
F:\temp\21610293.37280\Main.cpp(18) : error C2668: 'sqrt' : ambiguous call to overloaded function
        math.h(581): could be 'long double sqrt(long double)'
        math.h(533): or       'float sqrt(float)'
        math.h(128): or       'double sqrt(double)'
        while trying to match the argument list '(int)'

