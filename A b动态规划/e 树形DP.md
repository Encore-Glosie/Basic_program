# [285. 没有上司的舞会 - AcWing题库](https://www.acwing.com/problem/content/287/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
#define ll long long
const int N=6e3+5;
int f[N][2],ne[N],e[N],h[N],idx,hp[N];
bool fa[N];
void add(int a,int b){
    e[idx]=b;
    ne[idx]=h[a];
    h[a]=idx++;
}
void dfs(int u){
    f[u][1]=hp[u];
    for(int i=h[u];i!=-1;i=ne[i]){
        int j=e[i];
        dfs(j);
        f[u][0]+=max(f[j][0],f[j][1]);//不含根节点
        f[u][1]+=f[j][0];//含根节点
    }
}
void solve(){
    memset(h,-1,sizeof h);
   int n,a,b; cin>>n;
   for(int i=1;i<=n;++i)cin>>hp[i];
   for(int i=1;i<n;++i){
    cin>>a>>b;
    add(b,a);
    fa[a]=true;//记录每个节点是否有父节点
   }
   int root=1;
   while(fa[root])++root;//找没有父节点的点，即根节点
   dfs(root);
   cout<<max(f[root][0],f[root][1]);
   return ;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}
```
```cpp

```