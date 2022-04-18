---
title: 算法竞赛📖进阶指南练习 0x18
tag: [算法, C++, 数据结构]
date: 2021/04/08
---
# 括号画家 
入栈的时候先把对应的括号入栈，比如 遇到`(`先把`)`入栈，这样后面判断的时候，只要判断是不是一样`==`就行，妙啊！
BF做的，不一样就break
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
const int N = 100005;
char st[N],s[N];
int top,ans,t;
signed main() {
    scanf("%s",s);
    for(int i = 0; s[i]; i++){
        top = 0;
        for (int j = i; s[j]; j++) {
            if (s[j] == '(') st[++top] = ')';
            else if (s[j] == '[') st[++top] = ']';
            else if (s[j] == '{') st[++top] = '}';
            else if (!top || s[j] != st[top]) break;
            else{
                top--;
                if(!top) ans = max(ans,j - i + 1);
                // 更新一下最大的匹配长度
            }
        }
    }
    cout << ans << endl;
    return 0;
}

```
# POJ 2823 Sliding Window

这个题大方向想到了，但是没想到要删除队尾的元素来维护单调性。
后来测试数据的时候发现之前的写法有问题，想了一圈不知道应该改哪里，后来还是去搜了一下别人的思路，发现需要维护队尾的单调性。
为什么自己没想到捏？因为书没学进去，读了天书。
最后借鉴的标答的代码，写的真的简洁，比其他人的都短好多。

除了单调队列，这个是不是还可以用区间dp，线段树。但我觉得可能会超时吧。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
//之前还想着用list和queue做，想多了，list是真的 🉑️
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f


const int N = 1e6+5;
int n,k,a;
int maxa[N],maxt[N],ans1[N],maxl=0,maxr=0;
//数值,   控制窗口移动， 结果,  左区间, 右区间
int mina[N],mint[N],ans2[N],minl=0,minr=0;


int main()
{
    scanf("%d%d",&n,&k);
    for(int i=1;i<=n;i++){
        scanf("%d",&a);
        while(maxt[maxl] <= i - k && maxl < maxr) maxl++;
        while(mint[minl] <= i - k && minl < minr) minl++;
        // 让窗口滑动到i-k的位置
        while(maxa[maxr - 1] <= a && maxl < maxr) maxr--;
        //如果队尾元素比 a 更小的话，需要删除
        while(mina[minr - 1] >= a && minl < minr) minr--;
        
        maxa[maxr] = mina[minr] = a;
        //将a插入队尾
        maxt[maxr++] = mint[minr++] = i;
        //记录当前队尾的位置，左端点之后要右移
        ans1[i] = maxa[maxl];
        ans2[i] = mina[minl];
        //记录答案
    }
    
    for(int i = k;i <= n; i++)
        printf("%d ",ans2[i]);
    printf("\n");
    for(int i = k;i <= n; i++)
        printf("%d ",ans1[i]);
    printf("\n");
    return 0;
 }

```
# City Game
思路也很简单嘛，就是单调栈，矩形求面积的题。
不一样的是 底边不一样，我们可以枚举以n为底的矩形条求面积，最后取最大值。
我在借鉴代码的时候看了两个代码，写法不一样，搞得有点懵，最后还是自己又看了一遍书和标答写出来了。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f
#define ms(a, b) memset((a), (b), sizeof (a))

//const int N = 1e6+5;
int n,m;
char t;
bool a[1006][1006];
int h[1006],w[1006],st[1006],s,ans,res;

int f(int i){
    ans = 0;s = 0;
    for(int j = 1;j <= m;j++)
        if(a[i][j]) h[j]++;
        else h[j] = 0;
    
    for(int j = 1;j <= m + 1;j++){
        if(st[s] < h[j]){
            st[++s] = h[j];
            w[s] = 1;
            ans = max(ans, h[j]);
        }else{
            int num = 0;
            while(s && st[s] >= h[j]){
                num += w[s];
                ans = max(ans, st[s--] * num);
            }
            st[++s] = h[j];
            w[s] = ++num;
            ans = max(ans, st[s] * w[s]);
        }
    }
    return ans;
}


int main()
{
    int c;
    cin >> c;
    while(c--){
        ms(h, 0);
        ms(st,0);
        ms(w,0);
        ms(a,0);
        scanf("%d%d",&n,&m);
        for(int i = 1;i <= n; i++)
            for(int j = 1;j <= m; j++){
                cin >> t;
                a[i][j] = (t == 'F');
            }

        res = 0;
        for(int i = 1;i <= n;i++) res = max(res,f(i));
        cout << 3 * res  << endl;
    }
    return 0;
 }

```
# Subway tree systems
这个题是求树的同构，写法看了标答。
思路是对于 两棵树，如果有一样的最小表示法，那么就是一颗树。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f
#define ms(a, b) memset((a), (b), sizeof (a))

const int N = 1e5+5;
int a[N<<1],t;
string s1,s2;

string w(string s){
    vector<string> a;
    string f = "";
    int num = 0 ,t = 0;
    for(unsigned int i = 0; i< s.size(); i++){
        if(s[i] == '0') num ++;
        else num --;
        //num加减以后回到0，表示是回到原来的地方，也就是之前走过的那些是一段子树
        if(!num){
            if(i - 1 > t + 1)
                a.push_back("0" + w(s.substr(t + 1, i - 1 - t)) + "1");
                //递归到下一层，求出子树的最小表示法
            else a.push_back("01");
            t = i + 1;
        }
    }
    sort(a.begin(),a.end());//对一段子树排序
    for(int i = 0;i < a.size();i++)f += a[i];
    return f;
}

int main()
{
    scanf("%d",&t);
    while(t--){
        cin >> s1 >> s2;
        cout << (w(s1) == w(s2) ? "same" : "different") << endl;
    }
    return 0;
 }

```

# Necklace
通过O(n)的计算出两个字符串的最小表示法，然后用strcmp()比较一下
```cpp
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int N = 2e6+5;
char a[N], b[N];

int fun(char s[], int n){
    for(int i = 0; i < n; i++)s[n+i] = s[i];
    int i = 1, j =2,k;
    while(i <= n && j <= n){
        for(k = 0; k < n && s[i + k] == s[j + k]; k++);
        if(k == n)break;
        if(s[i + k] > s[j + k]){
            i += k + 1;
            if(i == j)i++;
        }
        else{
            j = j + k + 1;
            if(i == j) j++;
        }
    }
    return min(i, j);
}
int main(){
    scanf("%s%s",a, b);
    int la = strlen(a);
    int lb = strlen(b);
    if(la != lb){
        puts("No");
        return 0;
    }
    int n = la;
    la = fun(a, la); // 返回值la表示的是从a[la, la + n]是 a 的最小表示
    lb = fun(b, lb);
    a[la + n] = b[lb + n] = 0; // 在字符串的最后加上
	if (!strcmp(a + la, b + lb)) { // strcmp()比较是不是一样
		puts("Yes");
		puts(a + la);
	}
    else puts("No");
    return 0;
}
```
#  生日礼物
链表 + 优先队列

> 先把数据分成最长的连续小块，满足每个小块里面要么只有负数，要么只有整数，那么
> 最大的ans就是每个正数小块的和。但是题目上规定了小块的数量，所以你需要将某些
> 小块合成成一个小块，怎么合成呢？
>就是每次把负数小块里面值最大的找到，然后把它和它左右两个正数小块合成，这样两
>个整数小块就变成了一个小块（中间有一个负数）。
>这个我没做出来，抄的书上的代码

大佬的分析
这个我也没做出来，想来想去，还是答案写的好。
链表和树是我用的最不熟的部分，之后一定恶补！！
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f
#define ms(a, b) memset((a), (b), sizeof (a))

const int N = 1e5+5;
struct P{
    int p,c;
    bool operator <(const P x){
        return abs(c) > abs(x.c);
    }
};
priority_queue<P> q;
int a[N];
int nxt[N],prv[N],v[N];
int n,m,tot = 1,t,ans,cnt;
void del(int x) {
    v[x] = 0;
    prv[nxt[x]] = prv[x];
    nxt[prv[x]] = nxt[x];
}
int main()
{
    scanf("%d%d",&n,&m);
    for(int i=0;i<n;i++){
        scanf("%d",&t);
        if(t * a[tot] >= 0)a[tot] += t;
        else a[++tot] = t;
    }
    int ans = 0,cnt = 0;
    for(int i = 1;i <= tot;i++){
        P p;p.c = a[i];p.p = i;
        q.push(p);
        if(a[i] > 0){
            ans +=a[i];
            cnt++;
        }
        prv[i] = i - 1;
        nxt[i] = i + 1;
    }
    memset(v, 1, sizeof v);
    while(cnt > m){
        cnt--;
        P p = q.top();
        while(!v[p.p]){
            q.pop();p = q.top();
        }
        q.pop();
        if(prv[p.p] && nxt[p.p] != tot + 1)ans -= abs(a[p.p]);
        else if(a[p.p] > 0) ans -= a[p.p];
        else {
            cnt++;continue;
        }
        a[p.p] += a[prv[p.p]] + a[nxt[p.p]];
        del(prv[p.p]);del(nxt[p.p]);
        p.c  = a[p.p];
        q.push(p);
    }
    cout << ans << endl;
    return 0;
 }

```
# 双栈排序
思路是：染色法，二分图。

怪我太菜，慢慢想想不出来怎么写，还是要看答案。
还要想半天。最后借鉴了答案的写法。
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
#include <stack>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f
#define ms(a, b) memset((a), (b), sizeof (a))

const int N = 1e5+5;
int t,n,a[N];
int f[N],color[N];
bool g[N][N];

bool dfs(int u, int c)
{
    color[u] = c;
    for (int i = 1; i <= n; i++)
        if (g[u][i])
        {
            if (color[i] == c) return false;
            if (color[i] == -1 && !dfs(i, !c)) return false;
        }

    return true;
}

int main()
{
    scanf("%d",&t);
    while (t--) {
        scanf("%d",&n);
        for(int i = 1;i <= n;i++)scanf("%d", a+i);
        f[n + 1] = n + 1;
        ms(g, 0);
        for(int i = n; i; i--)f[i] = min(f[i + 1], a[i]);
        
        for(int i = 1;i <= n; i++)
            for(int j = i + 1;j <= n; j++)
                if(a[i] < a[j] && f[j + 1] < a[i])
                    g[i][j] = g[j][i] = 1;
        ms(color, -1);
        
        bool flag = 1;
        for(int i = 1;i <= n;i++)
            if(color[i] == -1 && !dfs(i, 0)){
                flag = 0;
                break;
            }
        if (!flag) {
            cout << 0 << endl;continue;
        }
        stack<int> stk1,stk2;
        int now = 1;
        for (int i = 1; i <= n; i++) {
            if(color[i] == 0){
                while (stk1.size() && stk1.top() == now) {
                    stk1.pop();cout << "b "; now++;
                }
                stk1.push(a[i]);
                cout << "a ";
            }
            else{
                while (true)
                    if (stk1.size() && stk1.top() == now)
                    {
                        stk1.pop();
                        cout << "b ";
                        now++;
                    }
                    else if (stk2.size() && stk2.top() == now)
                    {
                        stk2.pop();
                        cout << "d ";
                        now++;
                    }
                    else break;
                stk2.push(a[i]);
                cout << "c ";
            }
        }
        while (true)
            if (stk1.size() && stk1.top() == now)
            {
                stk1.pop();
                cout << "b ";
                now++;
            }
            else if (stk2.size() && stk2.top() == now)
            {
                stk2.pop();
                cout << "d ";
                now++;
            }
            else break;
        cout << endl;
        
    }
    return 0;
 }

```
# black box
```
【思路】

建立一个小堆和一个大堆。大堆用来存放第1..index-1大的数，其余数存放在大堆，小堆的堆顶元素便是我们要求出的第index大的数。
每次插入一个A(n)，必须保证大堆中数字数目不变，故先插入小堆中。若此时小堆堆顶小于大堆堆顶，则交换堆顶元素；每次Get()，输出小堆的堆顶元素，并将它并入大堆中。

```
来自别人的思路⬆️

来自标答的代码，
我不懂为什么q2的操作要加-号

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
#include <list>
#include <stack>
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f
#define ms(a, b) memset((a), (b), sizeof (a))

const int N = 1e5+5;
int a[N];
priority_queue<int> q1,q2;

int main()
{
    int m,n;
    cin >> m >> n;
    for(int i = 0; i < m; i++) scanf("%d",a + i);
    int t = 0;
    while(n--){
        int k;
        scanf("%d", &k);
        while (t < k) {
            q2.push(-a[t]);
            if(q1.size() && q1.top() > -q2.top()){
                int x = q1.top(),y = -q2.top();
                q1.pop();q2.pop();
                q1.push(y);q2.push(-x);
            }
            t++;
        }
        cout << -q2.top() << endl;
        q1.push(-q2.top());
        q2.pop();
    }
    
    return 0;
 }

```
