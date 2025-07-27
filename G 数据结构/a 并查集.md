  ```cpp
  不压缩路径的find：仅查找根节点，不修改路径
    int find(int x) {
        // 循环找到根节点（父节点等于自身）
        while (parent[x] != x) {
            x = parent[x];  // 只移动指针，不修改父节点
        }
        return x;
    }

	  带路径压缩的find：查找时将节点直接指向根节点
    int find(int x) {
        // 递归版本：将x的父节点直接设为根节点
        if (parent[x] != x) {
            parent[x] = find(parent[x]);  // 关键：修改父节点为根节点
        }
        return parent[x];
    }

	```
# [836. 合并集合 - AcWing题库](https://www.acwing.com/problem/content/838/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
const int N=1e5+7;
int p[N];
int find(int x){
    if(x!=p[x])p[x]=find(p[x]);
    return p[x];
}
void merge(int a,int b){
    int pa=find(a);
    int pb=find(b);
    if(pa!=pb)p[pa]=pb;
}
void query(int a,int b){
    if(find(a)==find(b))cout<<"Yes\n";
    else cout<<"No\n";
}
void solve(){
    int n,m;
    cin>>n>>m;
    for(int i=1;i<=n;++i)p[i]=i;
    while(m--){
        char op; cin>>op;
        int a,b; cin>>a>>b;
        if(op=='M')merge(a,b);
        else query(a,b);
    }
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
   while(T--)solve();
   return 0;
}
```

# [836. 合并集合 - AcWing题库](https://www.acwing.com/problem/content/838/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define int long long
#define ll long long
const int N=1e5+7;
int p[N],cnt[N];
int find(int x){
    if(x!=p[x])p[x]=find(p[x]);
    return p[x];
}
void solve(){
    int n,m;
    cin>>n>>m;
    for(int i=1;i<=n;++i)p[i]=i,cnt[i]=1;
    while(m--){
        string op; cin>>op;
        int a,b; 
        if(op=="C"){
            cin>>a>>b;
            if(find(a)!=find(b)){
                cnt[find(b)]+=cnt[find(a)];//合并连通块(数量)
                p[find(a)]=find(b);//合并根节点
            }
        }
        else if(op=="Q1"){
            cin>>a>>b;
            if(find(a)==find(b))cout<<"Yes\n";
            else cout<<"No\n";
        }
        else{
            cin>>a;
            cout<<cnt[find(a)]<<endl;
        }
    }
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
   while(T--)solve();
   return 0;
}
```
# [837. 连通块中点的数量 - AcWing题库](https://www.acwing.com/problem/content/839/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define int long long
#define ll long long
const int N=1e5+7;
int p[N],cnt[N];
int find(int x){
    if(x!=p[x])p[x]=find(p[x]);
    return p[x];
}
void solve(){
    int n,m;
    cin>>n>>m;
    for(int i=1;i<=n;++i)p[i]=i,cnt[i]=1;
    while(m--){
        string op; cin>>op;
        int a,b; 
        if(op=="C"){
            cin>>a>>b;
            if(find(a)!=find(b)){
                cnt[find(b)]+=cnt[find(a)];//合并连通块(数量)
                p[find(a)]=find(b);//合并根节点
            }
        }
        else if(op=="Q1"){
            cin>>a>>b;
            if(find(a)==find(b))cout<<"Yes\n";
            else cout<<"No\n";
        }
        else{
            cin>>a;
            cout<<cnt[find(a)]<<endl;
        }
    }
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
   while(T--)solve();
   return 0;
}
```
# [240. 食物链 - AcWing题库](https://www.acwing.com/problem/content/242/)
*一共三种关系：
余1：可以吃根节点
余2：可以被根节点吃
余0：与根节点是同类
*
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//#define ULL unsigned long long
//const int N=1e5+3,P=131;
const int N=5e4+10,M=N*31;
int n,m,d[N],p[N];
int find(int x){
    if(p[x]!=x){
        int t=find(p[x]);
        d[x]+=d[p[x]];//父节点
        p[x]=t;//p[x]=find(p[x]);//父节点=根节点
    }
    return p[x];
}
void solve(){
    cin>>n>>m;
    for(int i=1;i<=n;++i)p[i]=i;
    int res=0;
    while(m--){
        int t,x,y;
        cin>>t>>x>>y;
        if(x>n||y>n)++res;
        else{
            int px=find(x),py=find(y);
            if(t==1){
                if(px==py&&(d[x]-d[y])%3)++res;
                else if(px!=py){
                    p[px]=py;
                    d[px]=d[y]-d[x];//(d[x] + d[px]) ≡ (d[y] mod 3 )=(d[x]+d[px]-d[y])%3=0
                }
            }
            else{
                if(px==py&&(d[x]-d[y]-1)%3)++res;
                else if(px!=py){
                    p[px]=py;
                    d[px]=d[y]+1-d[x];
                }
            }
        }
    }
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