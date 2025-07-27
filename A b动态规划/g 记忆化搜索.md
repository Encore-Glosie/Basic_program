
####  记忆化搜索
==在传统的递归解法中，当函数需要多次调用自身时，可能会出现重复计算相同的子问题。这种情况下，记忆化搜索通过保存已计算过的结果，避免重复计算，从而提高程序的执行效率。==

# [901. 滑雪 - AcWing题库](https://www.acwing.com/problem/content/903/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
#define ll long long
const int N=3e2+5;
int h[N][N],f[N][N],n,m;
int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
int dp(int x,int y){
    int &v=f[x][y];
    if(v!=-1)return v;
    v=1;
    for(int i=0;i<4;++i){
        int a=x+dx[i],b=y+dy[i];
        if(a>=1&&a<=n&&b>=1&&b<=m&&h[a][b]<h[x][y])
        v=max(v,dp(a,b)+1);
    }
    return v;
}
void solve(){
   cin>>n>>m;
   for(int i=1;i<=n;++i)
        for(int j=1;j<=m;++j)
            cin>>h[i][j];
    memset(f,-1,sizeof f);
    int res=0;
    for(int i=1;i<=n;++i)
        for(int j=1;j<=m;++j)
            res=max(res,dp(i,j));
    cout<<res<<endl;   
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}
```

[P2548 - 路径计数 Ⅰ - ZJHUOJ](http://172.20.8.83/problem.php?id=2548)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int mod=1e9+7,mxn=1e3+5;
int dp[mxn][mxn],n,m;
int f(int x,int y){//dfs
    if(dp[x][y])return dp[x][y];
    if(x>1)dp[x][y]+=f(x-1,y);
    if(y>1)dp[x][y]+=f(x,y-1);
    return dp[x][y]%=mod;
}
signed main(){
 dp[1][1]=1;
 scanf("%lld%lld",&n,&m);
 printf("%lld\n",f(n,m));
 return 0;
}
```
#### DP
[P1084 - 子序列的和 Ⅲ - ZJHUOJ](http://172.20.8.83/problem.php?id=1084)
*（前 i 个数的和为 j ）
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int mxn=1e3+5,mod=1e9+7;
int dp[mxn][mxn],n; 
signed main(){
    dp[0][0]=1;
	for(int i=1;i<=1001;++i){
        for(int j=0;j<=1001;++j){//j不从0开始的话无法回到dp[0][0]
           dp[i][j]=dp[i-1][j];
           if(i<=j)dp[i][j]=(dp[i][j]+dp[i-1][j-i])%mod;//前i的数的和为j
        }
    }
	while(scanf("%lld",&n)==1)printf("%lld\n",dp[n][n]);
    return 0;
}
```