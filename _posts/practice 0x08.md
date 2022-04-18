---
title: 算法竞赛📖进阶指南练习 0x08
tag: [算法, C++]
date: 2021/04/08
---
# 算法竞赛进阶指南练习 0x08


# 1.The Pilots Brothers' refrigerator
> 对于某个点(x,y)，如果把这个点位置对应的行和列上每一个位置都进行一次操作（共7次操作），那么只有这个点变成了相反的点，其他点都不变，这个是可以证明的。
> 然后对于每个‘+’,按照上面的操作搞一次，就可以把每个‘+’,都变成’-’。记录每个点被操作的次数。这时候肯定有的点不只是被操作了一次，因为一个点操作偶数次都等于不操作，奇数次就相当于操作一次，这时候历遍每个点的操作次数，把奇数变成1，偶数变成0，这就是答案。
> 这个思路参考了 yingxiang720
> [原文链接](https://blog.csdn.net/Fawkess/article/details/105959342)

⬆️ 又是看了带佬的思路，对，这样才是正确解法。
多说一句，这里正确是因为刚好这个N是偶数，其他情况不可以。

顺着思路自己写了一遍 ⬇️
```cpp
#include <iostream>
#include <cstring>
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
typedef long long ll;

char a[10][10];
int s[10][10],res[20][2];

void f(int x,int y){
    for(int i=0;i<4;i++)
        s[x][i]++;
    for(int i=0;i<4;i++)
        s[i][y]++;
    s[x][y]--;
}

int main()
{
    for(int i=0;i<4;i++)
        for(int j=0;j<4;j++){
            cin >> a[i][j];
            if(a[i][j]=='+')f(i,j);
        }
    
    int ans=0;
    for(int i=0;i<4;i++)
        for(int j=0;j<4;j++)
            if(s[i][j]&1)
                res[ans][0] = i,res[ans++][1] = j;
                
    cout << ans << endl;
    for(int i=0;i<ans;i++)printf("%d %d\n",res[i][0]+1,res[i][1]+1);
    return 0;
 }

```

# 2.占卜DIY
思路很简单，模拟一遍就行，但是我自己写的太丑了，看懂别人的以后重写了一遍，妙啊，人都升华了。
[原文链接](https://blog.csdn.net/weixin_45508368/article/details/100558681)
```cpp
#include <iostream>
#include <cstring>
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
typedef long long ll;

const int N = 100;
int down[N][N],up[N];

int f(char t){
    if(t == 'A') return 1;
    if(t == '0') return 10;
    if(t == 'J') return 11;
    if(t == 'Q') return 12;
    if(t == 'K') return 13;
    return t - '0';
}

int main()
{
    char card[2];
    for (int i = 1; i <= 13; ++i)
    for (int j = 1; j <= 4; ++j) {
        scanf("%s", card);
        down[i][j] = f(card[0]);
    }
    int p=0;
    for(int i=1;i<=4;i++){
        p = down[13][i];
        while(p!=13){
            up[p]++;
            p = down[p][5-up[p]];
        }
    }
    int cnt=0;
    for(int i=1;i<=13;i++)
        if(up[i] == 4) cnt++;
    cout << cnt << endl;
    return 0;
 }
```
# 3.Fractal 
~~代码没了，就不写了~~ 
来补上了
```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
#include <map>
#include <unordered_map>
#include <stack>
#include <vector>
#include <typeinfo>
#include <set>
using namespace std;
#pragma GCC optimize(fast)
#define ll long long
#define INF 0x3f3f3f3f
#define ull unsigned long long
#define ms(a, b) memset((a), (b), sizeof (a))
#define readfile(a) freopen((a),"r",stdin)

int n;
const int N = 3000;
int s[N][N];
void f(int l, int x,int y){
    if(l == 1){
        s[x][y] = 1;
        return ;
    }
    int len = l / 3;
    f(len,x,y);
    f(len,x + 2 * len,y);
    f(len,x + len,y + len);
    f(len,x,y + 2 * len);
    f(len,x + 2 * len,y + 2 * len);
}

signed main() {
    int MAX_LEN = 2187;
	//提交的时候这里老是错，气死我了，拿计算器算了3^7为2187，数组开到2200左右就稳了.
    f(MAX_LEN,0,0);
    while (cin >> n && n!=-1) {
        int len = pow(3,n - 1);
        for(int i = 0; i < len;i++){
            for(int j = 0;j<len;j++)
                if(s[i][j]==1)printf("X");
                else printf(" ");
            puts("");
        }
        printf("-\n");
    }
    return 0;
}

```
# 4.Raid
这个题的知识点是 **平面最近点对**，解决的算法是**分治**，我第一遍写的时候就只想到了暴力，**TLE很正常**。其他办法也没想到，就算知道分治也没有思路，后来搜了一下 **平面最近点对** 的做法，才懂了怎么处理。最后照着标答看半天还不知道哪里写错了，最后的最后发现是dis函数的问题。我一开始写错还能过几个是真没想到的。

```cpp
return sqrt(a.x * a.x - b.x * b.x + a.y * a.y - b.y * b.y);
```

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
#define ll long long
typedef long double ld;

const double INF = 0x3f3f3f3f, eps = 0.000001;

const int N = 5e5+5;// 我看到一组测试数据的n是5w，才开到5e5+5，标答的开1e5+5也能过？
struct p{
    int x,y;
    bool z;
    bool operator < (const p &b)const{
            return x < b.x;
    }
}a[2*N];
int t,n;

double dis(p a,p b){
    if(a.z == b.z)return INF;
    return sqrt((ld)(a.x - b.x) * (a.x - b.x) + (ld)(a.y - b.y) * (a.y - b.y));
}

double DC(int l, int r){
    if(l == r) return INF;
    if(l + 1 == r) return dis(a[l], a[r]);
    
    int mid = (l + r) >> 1;
    double ans = min(DC(l, mid), DC(mid, r));
    for (int i = mid - 1; i >= l; i--) {
        if (a[mid].x - a[i].x + eps > ans) break;
        for (int j = mid + 1; j <= r; j++) {
            if (a[j].x - a[i].x + eps > ans) break;
            ans = min(ans, dis(a[i],a[j]));
        }
    }
    return ans;
}


int main()
{
    scanf("%d",&t);
    while (t--) {
        scanf("%d",&n);
        for(int i = 1;i <= n; i++){
            cin >> a[i].x >> a[i].y;
            a[i].z = 0;
        }
        for(int i = n + 1;i <= 2 * n;i++){
            cin >> a[i].x >> a[i].y;
            a[i].z = 1;
        }
        sort(a + 1, a + 2 * n + 1);
        printf("%.3f\n",DC(1, 2 * n));
    }
    
    return 0;
 }

```
后来在牛客网上又做了一遍，发现直接过一遍也行？
```cpp
    while (t--) {
        cin >> n;
        for(int i = 0;i < 2 * n;i++)
            scanf("%d%d",&a[i].x,&a[i].y),a[i].z = (i >= n);

        sort(a , a + 2 * n);
        double d = INF;
        for(int i = 1;i < 2 * n; i++)
            d = min(d,dis(a[i-1],a[i]));
        printf("%.3lf\n",d); 
    }
```


# 5.防线
这道题有个很关键的点就是只有一处是奇数个，位置是p，求出前缀和，那么**p之前**的都是**偶数**，**之后的**都是奇数。就可二分查找。

参考了答案的写法，每次查询的时候求一次前缀和的结果，不保存成数组。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f

const int N = 2e5+5;
int t,n;
int s[N],e[N],d[N];

int f(int a, int b, int c) {
    return (b >= a) ? ((b - a) / c + 1) : 0;
}

int get(int r){
    int ans = 0;
    for(int i = 1;i <= n; i++) ans += f(s[i], min(e[i], r), d[i]);
    return ans;
}

int main()
{
    scanf("%d",&t);
    while (t--) {
        int maxe = 0,mins = INF;
        scanf("%d",&n);
        for (int i = 1; i <= n; i++) {
            scanf("%d %d %d", &s[i], &e[i], &d[i]);
            mins = min(mins, s[i]);
            maxe = max(maxe, e[i]);
        }
        if(get(maxe) % 2 == 0){
            printf("There's no weakness.\n");continue;
        }
        int l = mins, r = maxe;
        while (l < r) {
            int mid = (l + r) >> 1;
            if (get(mid) % 2) r = mid;
            else l = mid + 1;
        }
        cout << l << " " << get(l) - get(l - 1) << endl;
    }
    
    
    return 0;
 }
```

# 6.Corral the Cows POJ3179
思路很简单嘛，预处理出二维前缀和，二分找到最小的围栏，每次二分暴力遍历所有方块（考虑边长为k的正方形内，最多有几个三叶草）。
中间要注意的是，需要离散化，我的代码没有写离散化部分，因为我太菜了。
```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
#include <map>
//#include <unordered_map>
#include <stack>
#include <vector>
#include <typeinfo>
#include <set>
using namespace std;
#pragma GCC optimize(fast)
#define ll long long
#define INF 0x3f3f3f3f
#define ull unsigned long long
#define ms(a, b) memset((a), (b), sizeof (a))
#define readfile(a) freopen((a),"r",stdin)

#define int ll
const int N = 555;
int sum[N][N], c, n;
int a[N][N], x, y;

int num(int x1,int y1,int x2, int y2){
    return sum[x2][y2] + sum[x1-1][y1-1] - sum[x1-1][y2] - sum[x2][y1-1];
}

bool check(int m){
    int ans = 0;
    for(int i = 1; i + m < N;i++)
        for(int j = 1; j + m < N;j++)
            ans = max(ans,num(i,j,i + m,j + m));
    
    return ans >= c;
}

signed main() {
    cin >> c >> n;
    for(int i = 1; i <= n; i++){
        scanf("%lld%lld",&x,&y);
        a[x][y] += 1;
    }
    
    for(int i = 1; i < N; i++)
        for(int j = 1; j < N; j++)
            sum[i][j] = sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1] + a[i][j];
    
    int l = 1, r = N, mid;
    while (l < r) {
        mid = (l + r) >> 1;
        if(check(mid))r = mid;
        else l = mid + 1;
    }
    cout << l << endl;
    
    return 0;
}

```


# 7.糖果传递
我又想了好久好久，awsl。
大佬的思路
```
设第𝑖个小朋友从他左边小朋友那里得到 𝑙𝑖 个糖果，向他右边的小朋友传递 𝑟𝑖 个糖果
（𝑙𝑖 与 𝑟𝑖 都可以为负数）
显然 𝑙𝑖=𝑟𝑖−1 ,特殊地 𝑙1=𝑟𝑛
设𝑝为最终每个小朋友手中的糖果数
则有 𝑙𝑖+𝑎𝑖−𝑟𝑖=𝑝 , 即 𝑟𝑖=𝑙𝑖+(𝑎𝑖−𝑝)
而我们又有 𝑙𝑖=𝑟𝑖−1
一直递归下去有 𝑟𝑖=𝑙1+(𝑎1−𝑝)+(𝑎2−𝑝)+(𝑎3−𝑝)+…+(𝑎𝑖−𝑝)
最终答案为 |𝑟1|+|𝑟2|+…+|𝑟𝑛|
我们可以记下 𝑎𝑖−𝑝 的前缀和为 𝑠𝑢𝑚𝑖
那么 𝑎𝑛𝑠=|𝑙1+𝑠𝑢𝑚1|+|𝑙1+𝑠𝑢𝑚2|+…+|𝑙1+𝑠𝑢𝑚𝑛|
绝对值是个美妙的东西，|𝑙1+𝑠𝑢𝑚𝑖| 可想为数轴上 −𝑙𝑖 与 𝑠𝑢𝑚𝑖 的距离
那么𝑎𝑛𝑠的最小值在 −𝑙1 取 𝑠𝑢𝑚𝑖 中位数时取到

求出𝑠𝑢𝑚𝑖及其中位数后计算即可.
```
下文的代码a数组在后面变成了sum数组，求和的过程，因为排序以后中位数左右两侧的 **距离** 是对称的，所以直接做差就行。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
#define ll long long

const int N = 1e6+6;
ll a[N],s,n;

int main()
{
    cin >> n;
    for(int i = 1;i <= n; i++){
        scanf("%lld",a+i);
        s+=a[i];
    }
    s /= n;
    for(int i = 1; i <= n; i++)a[i] = (a[i] - s) + a[i - 1];
    sort(a + 1 ,a + 1 + n);
    ll ans = 0; 	// 注意要用ll，不然会报错。
    for(int i = 1;i <= n / 2; i++)ans += a[n + 1 - i] - a[i];
    cout << ans << endl;
    
    return 0;
 }
```
# 8.Soldiers
还是要多看别人的代码，看了以后感觉人又升华了。
```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
#include <map>
#include <unordered_map>
#include <stack>
#include <vector>
#include <typeinfo>
#include <set>
using namespace std;
#pragma GCC optimize(fast)
#define ll long long
#define INF 0x3f3f3f3f
#define ull unsigned long long
#define ms(a, b) memset((a), (b), sizeof (a))
#define readfile(a) freopen((a),"r",stdin)


const int N = 1e5+5;
int x[N],y[N],n;
signed main() {
    cin >> n;
    for(int i = 1;i <= n; i++)scanf("%d%d",x + i,y + i);
    sort(x + 1, x + 1 + n);
    sort(y + 1, y + 1 + n);
    for(int i = 1; i <= n; i++) x[i] -= i;
    // 对于排好序的x，每个需要到自己的正确位置是 i,需要移动 pos - i
    // 顺序是连续的 1, 2, 3, 4...这样
    sort(x + 1, x + 1 + n);
    ll ans = 0;

    for(int i = 1; i <= n / 2; i++)
        ans += x[n - i + 1] - x[i] + y[n - i + 1] - y[i];

    cout << ans << endl;
    return 0;
}


```

# 9.Number Base Conversion
进制转换问题，我自己写的代码**问题一大推**，改都改不完。
最后看了标答的写法，发现可以直接转，不用拿十进制在中间转换。写法大概和我的一样，就是我的问题，我都不清楚错哪里了。就算中间转一下十进制也不会错啊。
唉，我太菜了。

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
#define ll long long

int cases,n,m;
const int N = 1e5+5;
char s[N];
char ans[N];

int f(char t){
    if(t>='0'&&t<='9') return t - '0';
    if(t>='A'&&t<='Z') return t - 'A' + 10;
    return t - 'a' + 36;
}
char f(int t){
    if(t>=0&&t<=9) return '0'+t;
    if(t>=10&&t<=35) return t + 'A' - 10;
    return t + 'a' - 36;
}

void number_base_conversion(){
    
    cin >> n >> m;
    scanf("%s",s);
    printf("%d %s\n%d ",n,s,m);
    
    int L = (int)strlen(s),t = (int)strlen(s),i,k;
    for(i=0;t;i++){
        k=0;
        for(int j=L-t;j<L;j++){
            k = k * n + f(s[j]);
            s[j] = f(k/m);
            k %= m;
        }
        ans[i] = f(k);
        while(t > 0 && s[L - t] == '0') t--;
    }
    while (--i >= 0)
        cout << ans[i];
    cout << "\n\n";
}

int main()
{
    cin >> cases;
    while(cases--)
        number_base_conversion();
    
    return 0;
 }
```
标答写的 f 函数是写成了两个数组，我觉得这种写法要好点，毕竟查询速度块

```cpp
int t = 0;
for (int i = '0'; i <= '9'; i++) {
		f[i] = t;
		ff[t++] = i;
	}
	for (int i = 'A'; i <= 'Z'; i++) {
		f[i] = t;
		ff[t++] = i;
	}
	for (int i = 'a'; i <= 'z'; i++) {
		f[i] = t;
		ff[t++] = i;
	}
```

# 10.Corral the Acrobats

```
题目中所求的是将最大风险最小化。那么对于某个牛i，假设它+它上面的牛的总重量为sum,
那么它的风险就为(sum-a[i].w)-a[i].s，即
sum-(a[i].w+a[i].s)，从这个式子可以看出，a[i].w+a[i].s越大越好，
所以我们将w+s的大小排序，大的放下面，小的放上面，然后遍历一遍，
找到最大风险，此时的最大风险就是最小的了。
```

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
using namespace std;
#define ll long long
#define INF 0x3f3f3f3f

const int N = 5e5+5;
int n;
ll s;
struct node{
    ll w,s;
    bool operator < (const node &b)const{
        return w+s > (b.w + b.s);
    }
}a[N];

int main()
{
    cin >> n;
    for(int i = 1;i <= n; i++){
        cin >> a[i].w >> a[i].s;
        s += a[i].w;
    }
    
    sort(a + 1, a + 1 + n);
    ll ans = -INF;
    for(int i = 1;i <= n; i++){
        s -= a[i].w;
        ans = max(ans,s-a[i].s);
    }
    cout << ans << endl;
    return 0;
 }
```
# 11.To the Max

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f

const int N = 1000;
int n,a[N][N],ans = 0,x[N];

int main()
{
    cin >> n;
    for(int i = 1;i <= n;i++)
        for(int j = 1;j <= n;j++)
            cin >> a[i][j];
    
    for(int i = 1;i <= n;i++){
        memset(x, 0, sizeof(x));
        for(int j = i; j <= n; j++){
            int num = 0;
            for(int k = 1;k <= n; k++){
                num += x[k] +=a[j][k];
                ans = max(ans,num);
                if(num < 0)num=0;
            }
        }
    }
    cout << ans << endl;
    
    return 0;
 }

```

# 12. Task
这个题，也是我能想出来的了，但是写不好，唉。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f

const int N = 1e5+5;
int n,m;
int num[N];
struct p{
    int x,y;
}a[N],b[N];
bool cmp(p &a,p &b){
    if(a.x != b.x)return a.x < b.x;
    return a.y < b.y;
}

ll ans;
int cnt;
int main()
{
    while(scanf("%d%d",&n,&m)!=EOF){
        for(int i=0;i<n;i++)scanf("%d%d", &a[i].x, &a[i].y);
        for(int i=0;i<m;i++)scanf("%d%d", &b[i].x, &b[i].y);
        sort(a, a + n, cmp);
        sort(b, b + m, cmp);
        int j = 0;
        for(int i=0;i<m;i++){
            while (j < n && a[j].x > b[j].x) num[a[j++].y]++;
            for(int k=b[i].y;k<100;k++)
                if(num[k]){
                    num[k]--;
                    cnt ++;
                    ans += 500 * b[k].x + 2 * b[k].y;
                }
                    
        }

        printf("%d %lld",cnt,ans);
        cnt = ans = 0;
        memset(num, 0, sizeof num);
    }
    return 0;
 }

```
