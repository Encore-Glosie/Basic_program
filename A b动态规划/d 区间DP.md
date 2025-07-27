DP分析：
1. 集合：将区间看作一堆方案的集合
2. 属性：每个子集取min或max就得到整个集合的min或max 
# [282. 石子合并 - AcWing题库](https://www.acwing.com/problem/content/284/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
#define ll long long
const int N = 3e2+7,inf=0x3f3f3f3f;
int f[N][N];
int s[N];
int n;
void solve(){
    cin>>n;
    for(int i=1;i<=n;++i)cin>>s[i],s[i]+=s[i-1];
    for(int len=2;len<=n;++len)
        for(int i=1;i+len-1<=n;++i){
            int j=i+len-1; f[i][j]=inf;
            for(int k=i;k<j;++k)
            f[i][j]=min(f[i][j],f[i][k]+f[k+1][j]+s[j]-s[i-1]);
        }
    cout<<f[1][n]<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}

```
# [900. 整数划分 - AcWing题库](https://www.acwing.com/problem/content/902/)
```cpp

```