*完全背包做法：
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
动态规划：

![[Pasted image 20250727001453.png]]


```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
#define ll long long
const int N=1e3+5,mod=1e9+7;
int f[N][N];
void solve(){
    int n; cin>>n;
    f[0][0]=1;//总和是i恰好表示j个数
    for(int i=1;i<=n;++i)
        for(int j=1;j<=i;++j)
            f[i][j]=(f[i-1][j-1]+f[i-j][j])%mod;
    int ans=0;
    for(int j=1;j<=n;++j)ans=(ans+f[n][j])%mod;
    cout<<ans<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}
```