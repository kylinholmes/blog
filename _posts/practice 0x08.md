---
title: ç®æ³ç«èµðè¿é¶æåç»ä¹  0x08
tag: [ç®æ³, C++]
date: 2021/04/08
---
# ç®æ³ç«èµè¿é¶æåç»ä¹  0x08


# 1.The Pilots Brothers' refrigerator
> å¯¹äºæä¸ªç¹(x,y)ï¼å¦ææè¿ä¸ªç¹ä½ç½®å¯¹åºçè¡ååä¸æ¯ä¸ä¸ªä½ç½®é½è¿è¡ä¸æ¬¡æä½ï¼å±7æ¬¡æä½ï¼ï¼é£ä¹åªæè¿ä¸ªç¹åæäºç¸åçç¹ï¼å¶ä»ç¹é½ä¸åï¼è¿ä¸ªæ¯å¯ä»¥è¯æçã
> ç¶åå¯¹äºæ¯ä¸ªâ+â,æç§ä¸é¢çæä½æä¸æ¬¡ï¼å°±å¯ä»¥ææ¯ä¸ªâ+â,é½åæâ-âãè®°å½æ¯ä¸ªç¹è¢«æä½çæ¬¡æ°ãè¿æ¶åè¯å®æçç¹ä¸åªæ¯è¢«æä½äºä¸æ¬¡ï¼å ä¸ºä¸ä¸ªç¹æä½å¶æ°æ¬¡é½ç­äºä¸æä½ï¼å¥æ°æ¬¡å°±ç¸å½äºæä½ä¸æ¬¡ï¼è¿æ¶ååéæ¯ä¸ªç¹çæä½æ¬¡æ°ï¼æå¥æ°åæ1ï¼å¶æ°åæ0ï¼è¿å°±æ¯ç­æ¡ã
> è¿ä¸ªæè·¯åèäº yingxiang720
> [åæé¾æ¥](https://blog.csdn.net/Fawkess/article/details/105959342)

â¬ï¸ åæ¯çäºå¸¦ä½¬çæè·¯ï¼å¯¹ï¼è¿æ ·ææ¯æ­£ç¡®è§£æ³ã
å¤è¯´ä¸å¥ï¼è¿éæ­£ç¡®æ¯å ä¸ºåå¥½è¿ä¸ªNæ¯å¶æ°ï¼å¶ä»æåµä¸å¯ä»¥ã

é¡ºçæè·¯èªå·±åäºä¸é â¬ï¸
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

# 2.å åDIY
æè·¯å¾ç®åï¼æ¨¡æä¸éå°±è¡ï¼ä½æ¯æèªå·±åçå¤ªä¸äºï¼çæå«äººçä»¥åéåäºä¸éï¼å¦åï¼äººé½ååäºã
[åæé¾æ¥](https://blog.csdn.net/weixin_45508368/article/details/100558681)
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
~~ä»£ç æ²¡äºï¼å°±ä¸åäº~~ 
æ¥è¡¥ä¸äº
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
	//æäº¤çæ¶åè¿éèæ¯éï¼æ°æ­»æäºï¼æ¿è®¡ç®å¨ç®äº3^7ä¸º2187ï¼æ°ç»å¼å°2200å·¦å³å°±ç¨³äº.
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
è¿ä¸ªé¢çç¥è¯ç¹æ¯ **å¹³é¢æè¿ç¹å¯¹**ï¼è§£å³çç®æ³æ¯**åæ²»**ï¼æç¬¬ä¸éåçæ¶åå°±åªæ³å°äºæ´åï¼**TLEå¾æ­£å¸¸**ãå¶ä»åæ³ä¹æ²¡æ³å°ï¼å°±ç®ç¥éåæ²»ä¹æ²¡ææè·¯ï¼åæ¥æäºä¸ä¸ **å¹³é¢æè¿ç¹å¯¹** çåæ³ï¼ææäºæä¹å¤çãæåç§çæ ç­çåå¤©è¿ä¸ç¥éåªéåéäºï¼æåçæååç°æ¯diså½æ°çé®é¢ãæä¸å¼å§åéè¿è½è¿å ä¸ªæ¯çæ²¡æ³å°çã

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

const int N = 5e5+5;// æçå°ä¸ç»æµè¯æ°æ®çnæ¯5wï¼æå¼å°5e5+5ï¼æ ç­çå¼1e5+5ä¹è½è¿ï¼
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
åæ¥å¨çå®¢ç½ä¸ååäºä¸éï¼åç°ç´æ¥è¿ä¸éä¹è¡ï¼
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


# 5.é²çº¿
è¿éé¢æä¸ªå¾å³é®çç¹å°±æ¯åªæä¸å¤æ¯å¥æ°ä¸ªï¼ä½ç½®æ¯pï¼æ±åºåç¼åï¼é£ä¹**pä¹å**çé½æ¯**å¶æ°**ï¼**ä¹åç**é½æ¯å¥æ°ãå°±å¯äºåæ¥æ¾ã

åèäºç­æ¡çåæ³ï¼æ¯æ¬¡æ¥è¯¢çæ¶åæ±ä¸æ¬¡åç¼åçç»æï¼ä¸ä¿å­ææ°ç»ã
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
æè·¯å¾ç®ååï¼é¢å¤çåºäºç»´åç¼åï¼äºåæ¾å°æå°çå´æ ï¼æ¯æ¬¡äºåæ´åéåæææ¹åï¼èèè¾¹é¿ä¸ºkçæ­£æ¹å½¢åï¼æå¤æå ä¸ªä¸å¶èï¼ã
ä¸­é´è¦æ³¨æçæ¯ï¼éè¦ç¦»æ£åï¼æçä»£ç æ²¡æåç¦»æ£åé¨åï¼å ä¸ºæå¤ªèäºã
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


# 7.ç³æä¼ é
æåæ³äºå¥½ä¹å¥½ä¹ï¼awslã
å¤§ä½¬çæè·¯
```
è®¾ç¬¬ðä¸ªå°æåä»ä»å·¦è¾¹å°æåé£éå¾å° ðð ä¸ªç³æï¼åä»å³è¾¹çå°æåä¼ é ðð ä¸ªç³æ
ï¼ðð ä¸ ðð é½å¯ä»¥ä¸ºè´æ°ï¼
æ¾ç¶ ðð=ððâ1 ,ç¹æ®å° ð1=ðð
è®¾ðä¸ºæç»æ¯ä¸ªå°æåæä¸­çç³ææ°
åæ ðð+ððâðð=ð , å³ ðð=ðð+(ððâð)
èæä»¬åæ ðð=ððâ1
ä¸ç´éå½ä¸å»æ ðð=ð1+(ð1âð)+(ð2âð)+(ð3âð)+â¦+(ððâð)
æç»ç­æ¡ä¸º |ð1|+|ð2|+â¦+|ðð|
æä»¬å¯ä»¥è®°ä¸ ððâð çåç¼åä¸º ð ð¢ðð
é£ä¹ ððð =|ð1+ð ð¢ð1|+|ð1+ð ð¢ð2|+â¦+|ð1+ð ð¢ðð|
ç»å¯¹å¼æ¯ä¸ªç¾å¦çä¸è¥¿ï¼|ð1+ð ð¢ðð| å¯æ³ä¸ºæ°è½´ä¸ âðð ä¸ ð ð¢ðð çè·ç¦»
é£ä¹ððð çæå°å¼å¨ âð1 å ð ð¢ðð ä¸­ä½æ°æ¶åå°

æ±åºð ð¢ððåå¶ä¸­ä½æ°åè®¡ç®å³å¯.
```
ä¸æçä»£ç aæ°ç»å¨åé¢åæäºsumæ°ç»ï¼æ±åçè¿ç¨ï¼å ä¸ºæåºä»¥åä¸­ä½æ°å·¦å³ä¸¤ä¾§ç **è·ç¦»** æ¯å¯¹ç§°çï¼æä»¥ç´æ¥åå·®å°±è¡ã
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
    ll ans = 0; 	// æ³¨æè¦ç¨llï¼ä¸ç¶ä¼æ¥éã
    for(int i = 1;i <= n / 2; i++)ans += a[n + 1 - i] - a[i];
    cout << ans << endl;
    
    return 0;
 }
```
# 8.Soldiers
è¿æ¯è¦å¤çå«äººçä»£ç ï¼çäºä»¥åæè§äººåååäºã
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
    // å¯¹äºæå¥½åºçxï¼æ¯ä¸ªéè¦å°èªå·±çæ­£ç¡®ä½ç½®æ¯ i,éè¦ç§»å¨ pos - i
    // é¡ºåºæ¯è¿ç»­ç 1, 2, 3, 4...è¿æ ·
    sort(x + 1, x + 1 + n);
    ll ans = 0;

    for(int i = 1; i <= n / 2; i++)
        ans += x[n - i + 1] - x[i] + y[n - i + 1] - y[i];

    cout << ans << endl;
    return 0;
}


```

# 9.Number Base Conversion
è¿å¶è½¬æ¢é®é¢ï¼æèªå·±åçä»£ç **é®é¢ä¸å¤§æ¨**ï¼æ¹é½æ¹ä¸å®ã
æåçäºæ ç­çåæ³ï¼åç°å¯ä»¥ç´æ¥è½¬ï¼ä¸ç¨æ¿åè¿å¶å¨ä¸­é´è½¬æ¢ãåæ³å¤§æ¦åæçä¸æ ·ï¼å°±æ¯æçé®é¢ï¼æé½ä¸æ¸æ¥éåªéäºãå°±ç®ä¸­é´è½¬ä¸ä¸åè¿å¶ä¹ä¸ä¼éåã
åï¼æå¤ªèäºã

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
æ ç­åç f å½æ°æ¯åæäºä¸¤ä¸ªæ°ç»ï¼æè§å¾è¿ç§åæ³è¦å¥½ç¹ï¼æ¯ç«æ¥è¯¢éåº¦å

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
é¢ç®ä¸­ææ±çæ¯å°æå¤§é£é©æå°åãé£ä¹å¯¹äºæä¸ªçiï¼åè®¾å®+å®ä¸é¢çççæ»ééä¸ºsum,
é£ä¹å®çé£é©å°±ä¸º(sum-a[i].w)-a[i].sï¼å³
sum-(a[i].w+a[i].s)ï¼ä»è¿ä¸ªå¼å­å¯ä»¥çåºï¼a[i].w+a[i].sè¶å¤§è¶å¥½ï¼
æä»¥æä»¬å°w+sçå¤§å°æåºï¼å¤§çæ¾ä¸é¢ï¼å°çæ¾ä¸é¢ï¼ç¶åéåä¸éï¼
æ¾å°æå¤§é£é©ï¼æ­¤æ¶çæå¤§é£é©å°±æ¯æå°çäºã
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
è¿ä¸ªé¢ï¼ä¹æ¯æè½æ³åºæ¥çäºï¼ä½æ¯åä¸å¥½ï¼åã
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
