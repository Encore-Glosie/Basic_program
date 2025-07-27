# [全球变暖 - 洛谷](https://www.luogu.com.cn/problem/P8662)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
const int mxn=1e2;
char s[mxn][mxn];
int dx[5]={0,0,-1,1};
int dy[5]={1,-1,0,0};
int n,ans,vis[mxn][mxn],f;
struct node{
  int x;
  int y;
};
queue<node>q;
//bfs
void bfs(int i,int j){
  q.push({i,j});
  vis[i][j]=1;
  while(!q.empty()){
       node now=q.front();
        q.pop();            //OMG一整块连接着的如果没有高地就会被淹没，左上角作为一块地被淹没
        if(s[now.x-1][now.y]=='#'&&s[now.x+1][now.y]=='#'&&s[now.x][now.y-1]=='#'&&s[now.x][now.y+1]=='#')f=1;            
        for(int i=0;i<4;++i){
          int x=now.x+dx[i];
          int y=now.y+dy[i]; 
          if(!vis[x][y]&&s[x][y]=='#'){
            vis[x][y]=1;
            node nex;
            nex.x=x;
            nex.y=y;
            q.push(nex);         
          }
      }
  }
}
void solve(){
     cin>>n;
     for(int i=1;i<=n;++i)cin>>s[i]+1;
      for(int i=1;i<=n;++i)
      for(int j=1;j<=n;++j){
        if(!vis[i][j]&&s[i][j]=='#'){
          f=0;//假设没有高地
          bfs(i,j);
        if(f==0)++ans;//若f为1证明有高地
        }
      }
      cout<<ans<<endl;
    return ;
}
signed main(){
  ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
   int T=1;
  //cin>>T;
  while(T--)solve();
  return 0;
}
dfs代码
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
const int mxn=1e3+10;
char s[mxn][mxn];
int dx[5]={0,0,-1,1};
int dy[5]={1,-1,0,0};
int n,ans,vis[mxn][mxn],f;
void dfs(int i,int j){
  vis[i][j]=1;
        if(s[i-1][j]=='#'&&s[i+1][j]=='#'&&s[i][j-1]=='#'&&s[i][j+1]=='#')f=1;//不要return，因为要继续搜索周围的陆地并做上标记
        for(int k=0;k<=4;++k){
          int x=i+dx[k];
          int y=j+dy[k];
          if(!vis[x][y]&&s[i][j]=='#')dfs(x,y);         
        }
  return ;
}
void solve(){
     cin>>n;
     for(int i=1;i<=n;++i)cin>>s[i]+1;
      for(int i=1;i<=n;++i)
      for(int j=1;j<=n;++j){
        if(!vis[i][j]&&s[i][j]=='#'){
          f=0;//假设没有高地
          dfs(i,j);
        if(f==0)++ans;//若f为1证明有高地
        }
      }
      cout<<ans<<endl;
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
## [P2626 - 图中点的层次 - ZJHUOJ](http://172.20.8.83/problem.php?id=2626)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
const int inf=0x3f3f3f3f;
const int N=1e5+5;
int  n,h[N],e[N],ne[N],st[N],dist[N],idx,ans;
void add(int a,int b){
    e[idx]=b, ne[idx]=h[a], h[a]=idx++;
}
void bfs(){
    queue<int>q;
    q.push(1); st[1]=1; dist[1]=0;
    while(!q.empty()){
        int t=q.front(); 
        q.pop();
        for(int i=h[t];i!=-1;i=ne[i]){
            int j=e[i];
            if(!st[j]){
            dist[j]=dist[t]+1;
            q.push(j); st[j]=1;
            }
        }
    } 
}
void solve(){
    memset(h,-1,sizeof h); memset(dist,inf,sizeof dist);
    int m,a,b; cin>>n>>m;
    for(int i=1;i<=m;++i){
        cin>>a>>b;
        add(a,b); 
    }
    bfs();
    cout<<(dist[n]==inf?-1:dist[n])<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
   // cin>>T;
    while(T--)solve();
    return 0;
}

```