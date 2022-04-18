---
title: CodeForces EDU 89 div.2 D
tag: [算法, C++, CodeForces]
date: 2021/04/08
---

这个题其实不难，想一下就容易想到了，但是我没想到😇
巨佬的[原文](https://blog.csdn.net/Fawkess/article/details/106712930)
```cpp
const int N = 5e5+5;
const int M = 1e7+7;
int n;
int a[N],b[N],c[N],L=0;
int v[M];
void prime(int n){
    for(int i=2;i<=n;i++){
        if(v[i]==1)continue;
        for(int j=i*2;j<=n;j+=i)
            v[j] = 1;
    }
}
int main()
{
    scanf("%d",&n);
    prime(M);
    for(int i=0;i<n;i++)scanf("%d",a+i);
    for(int i=0;i<n;i++){
        if(v[a[i]]==0){
            b[L] = c[L] = -1;
            L++;
            continue;
        }
        b[L] = a[i];
        int j=2;
        for(;j<=a[i];j++){
            if(a[i]%j==0)break;
        }
        while(b[L]%j==0)b[L]/=j;
        if(b[L]==1){
            b[L] = c[L] = -1;
            L++;
            continue;
        }
        c[L++] = j;
    }
    
    for(int i=0;i<L;i++)printf("%d ",b[i]);
    printf("\n");
    for(int i=0;i<L;i++)printf("%d ",c[i]);
    printf("\n");
    
    return 0;
 }
 //我的
```
关键是代码写的，和大佬的差距就是天壤之别，又简洁，没有多余的废话。
```cpp
const int N = 1e7 + 10;
int t, n, a[500050], d[500050], f[N];
int main() {
	f[1] = 2; 
	for (int i = 2; i < N; i++) 
		f[i] = i;
	for (int i = 2; i*i < N; i++)
		if (f[i] == i)
			for (int j = i * i; j < N; j += i)
				if (f[j] == j)
					f[j] = i;
	
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
		for (scanf("%d", a + i), d[i] = a[i];
		d[i] % f[a[i]] == 0; 
			d[i] /= f[a[i]]);

	for (int i = 0; i < n; i++) 
		printf("%d ", d[i] > 1 ? d[i] : -1);
	printf("\n");
	for (int i = 0; i < n; i++)
		printf("%d ", d[i] > 1 ? f[a[i]] : -1);

	return 0;
}
// 差别，高下立判
```
