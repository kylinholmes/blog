---
title: ç®æ³ç«èµðè¿é¶æåç»ä¹  0x18
tag: [ç®æ³, C++, æ°æ®ç»æ]
date: 2021/04/08
---
# æ¬å·ç»å®¶ 
å¥æ çæ¶ååæå¯¹åºçæ¬å·å¥æ ï¼æ¯å¦ éå°`(`åæ`)`å¥æ ï¼è¿æ ·åé¢å¤æ­çæ¶åï¼åªè¦å¤æ­æ¯ä¸æ¯ä¸æ ·`==`å°±è¡ï¼å¦åï¼
BFåçï¼ä¸ä¸æ ·å°±break
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
                // æ´æ°ä¸ä¸æå¤§çå¹éé¿åº¦
            }
        }
    }
    cout << ans << endl;
    return 0;
}

```
# POJ 2823 Sliding Window

è¿ä¸ªé¢å¤§æ¹åæ³å°äºï¼ä½æ¯æ²¡æ³å°è¦å é¤éå°¾çåç´ æ¥ç»´æ¤åè°æ§ã
åæ¥æµè¯æ°æ®çæ¶ååç°ä¹åçåæ³æé®é¢ï¼æ³äºä¸åä¸ç¥éåºè¯¥æ¹åªéï¼åæ¥è¿æ¯å»æäºä¸ä¸å«äººçæè·¯ï¼åç°éè¦ç»´æ¤éå°¾çåè°æ§ã
ä¸ºä»ä¹èªå·±æ²¡æ³å°æï¼å ä¸ºä¹¦æ²¡å­¦è¿å»ï¼è¯»äºå¤©ä¹¦ã
æååé´çæ ç­çä»£ç ï¼åçççç®æ´ï¼æ¯å¶ä»äººçé½ç­å¥½å¤ã

é¤äºåè°éåï¼è¿ä¸ªæ¯ä¸æ¯è¿å¯ä»¥ç¨åºé´dpï¼çº¿æ®µæ ãä½æè§å¾å¯è½ä¼è¶æ¶å§ã
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
//ä¹åè¿æ³çç¨liståqueueåï¼æ³å¤äºï¼listæ¯çç ðï¸
using namespace std;
#define ll long long
typedef long double ld;
#define INF 0x3f3f3f3f


const int N = 1e6+5;
int n,k,a;
int maxa[N],maxt[N],ans1[N],maxl=0,maxr=0;
//æ°å¼,   æ§å¶çªå£ç§»å¨ï¼ ç»æ,  å·¦åºé´, å³åºé´
int mina[N],mint[N],ans2[N],minl=0,minr=0;


int main()
{
    scanf("%d%d",&n,&k);
    for(int i=1;i<=n;i++){
        scanf("%d",&a);
        while(maxt[maxl] <= i - k && maxl < maxr) maxl++;
        while(mint[minl] <= i - k && minl < minr) minl++;
        // è®©çªå£æ»å¨å°i-kçä½ç½®
        while(maxa[maxr - 1] <= a && maxl < maxr) maxr--;
        //å¦æéå°¾åç´ æ¯ a æ´å°çè¯ï¼éè¦å é¤
        while(mina[minr - 1] >= a && minl < minr) minr--;
        
        maxa[maxr] = mina[minr] = a;
        //å°aæå¥éå°¾
        maxt[maxr++] = mint[minr++] = i;
        //è®°å½å½åéå°¾çä½ç½®ï¼å·¦ç«¯ç¹ä¹åè¦å³ç§»
        ans1[i] = maxa[maxl];
        ans2[i] = mina[minl];
        //è®°å½ç­æ¡
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
æè·¯ä¹å¾ç®ååï¼å°±æ¯åè°æ ï¼ç©å½¢æ±é¢ç§¯çé¢ã
ä¸ä¸æ ·çæ¯ åºè¾¹ä¸ä¸æ ·ï¼æä»¬å¯ä»¥æä¸¾ä»¥nä¸ºåºçç©å½¢æ¡æ±é¢ç§¯ï¼æååæå¤§å¼ã
æå¨åé´ä»£ç çæ¶åçäºä¸¤ä¸ªä»£ç ï¼åæ³ä¸ä¸æ ·ï¼æå¾æç¹æµï¼æåè¿æ¯èªå·±åçäºä¸éä¹¦åæ ç­ååºæ¥äºã
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
è¿ä¸ªé¢æ¯æ±æ çåæï¼åæ³çäºæ ç­ã
æè·¯æ¯å¯¹äº ä¸¤æ£µæ ï¼å¦ææä¸æ ·çæå°è¡¨ç¤ºæ³ï¼é£ä¹å°±æ¯ä¸é¢æ ã
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
        //numå åä»¥ååå°0ï¼è¡¨ç¤ºæ¯åå°åæ¥çå°æ¹ï¼ä¹å°±æ¯ä¹åèµ°è¿çé£äºæ¯ä¸æ®µå­æ 
        if(!num){
            if(i - 1 > t + 1)
                a.push_back("0" + w(s.substr(t + 1, i - 1 - t)) + "1");
                //éå½å°ä¸ä¸å±ï¼æ±åºå­æ çæå°è¡¨ç¤ºæ³
            else a.push_back("01");
            t = i + 1;
        }
    }
    sort(a.begin(),a.end());//å¯¹ä¸æ®µå­æ æåº
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
éè¿O(n)çè®¡ç®åºä¸¤ä¸ªå­ç¬¦ä¸²çæå°è¡¨ç¤ºæ³ï¼ç¶åç¨strcmp()æ¯è¾ä¸ä¸
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
    la = fun(a, la); // è¿åå¼laè¡¨ç¤ºçæ¯ä»a[la, la + n]æ¯ a çæå°è¡¨ç¤º
    lb = fun(b, lb);
    a[la + n] = b[lb + n] = 0; // å¨å­ç¬¦ä¸²çæåå ä¸
	if (!strcmp(a + la, b + lb)) { // strcmp()æ¯è¾æ¯ä¸æ¯ä¸æ ·
		puts("Yes");
		puts(a + la);
	}
    else puts("No");
    return 0;
}
```
#  çæ¥ç¤¼ç©
é¾è¡¨ + ä¼åéå

> åææ°æ®åææé¿çè¿ç»­å°åï¼æ»¡è¶³æ¯ä¸ªå°åéé¢è¦ä¹åªæè´æ°ï¼è¦ä¹åªææ´æ°ï¼é£ä¹
> æå¤§çanså°±æ¯æ¯ä¸ªæ­£æ°å°åçåãä½æ¯é¢ç®ä¸è§å®äºå°åçæ°éï¼æä»¥ä½ éè¦å°æäº
> å°ååææä¸ä¸ªå°åï¼æä¹åæå¢ï¼
>å°±æ¯æ¯æ¬¡æè´æ°å°åéé¢å¼æå¤§çæ¾å°ï¼ç¶åæå®åå®å·¦å³ä¸¤ä¸ªæ­£æ°å°ååæï¼è¿æ ·ä¸¤
>ä¸ªæ´æ°å°åå°±åæäºä¸ä¸ªå°åï¼ä¸­é´æä¸ä¸ªè´æ°ï¼ã
>è¿ä¸ªææ²¡ååºæ¥ï¼æçä¹¦ä¸çä»£ç 

å¤§ä½¬çåæ
è¿ä¸ªæä¹æ²¡ååºæ¥ï¼æ³æ¥æ³å»ï¼è¿æ¯ç­æ¡åçå¥½ã
é¾è¡¨åæ æ¯æç¨çæä¸ççé¨åï¼ä¹åä¸å®æ¶è¡¥ï¼ï¼
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
# åæ æåº
æè·¯æ¯ï¼æè²æ³ï¼äºåå¾ã

æªæå¤ªèï¼æ¢æ¢æ³æ³ä¸åºæ¥æä¹åï¼è¿æ¯è¦çç­æ¡ã
è¿è¦æ³åå¤©ãæååé´äºç­æ¡çåæ³ã
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
ãæè·¯ã

å»ºç«ä¸ä¸ªå°å åä¸ä¸ªå¤§å ãå¤§å ç¨æ¥å­æ¾ç¬¬1..index-1å¤§çæ°ï¼å¶ä½æ°å­æ¾å¨å¤§å ï¼å°å çå é¡¶åç´ ä¾¿æ¯æä»¬è¦æ±åºçç¬¬indexå¤§çæ°ã
æ¯æ¬¡æå¥ä¸ä¸ªA(n)ï¼å¿é¡»ä¿è¯å¤§å ä¸­æ°å­æ°ç®ä¸åï¼æåæå¥å°å ä¸­ãè¥æ­¤æ¶å°å å é¡¶å°äºå¤§å å é¡¶ï¼åäº¤æ¢å é¡¶åç´ ï¼æ¯æ¬¡Get()ï¼è¾åºå°å çå é¡¶åç´ ï¼å¹¶å°å®å¹¶å¥å¤§å ä¸­ã

```
æ¥èªå«äººçæè·¯â¬ï¸

æ¥èªæ ç­çä»£ç ï¼
æä¸æä¸ºä»ä¹q2çæä½è¦å -å·

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
