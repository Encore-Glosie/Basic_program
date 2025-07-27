## K
```cpp
- e[i][j]：表示第 i 个房间第 j 个门通向哪个房间（最多 3 个门）；
- d[i]：房间 i 有几个门；
- ans[i][j]：表示从房间 i 的第 j个门出发，最终可以走过多少条走廊；
- vis[i][j]：表示房间 i 的第 j 个门是否已经访问过（防止死循环）；
- mp[u][v]：记录是否已经走过边 (u, v)（因为每条边只能计一次）。
- 
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int N = 2e5+10;
int e[N][5],d[N],ans[N][5],vis[N][5];
map<int,map<int,bool>>mp;
int dfs(int u,int num,int cnt){
	vis[u][num] = 1;
	int v = e[u][num];
	int nex;
	for(int i=0;i<d[v];i++){
		if(e[v][i] == u)
			nex = (i + 1) % d[v];
	} 
	int st = mp[u][v];
	mp[u][v] = 1;
	mp[v][u] = 1;
	if(vis[v][nex]){
		return ans[u][num] = !st + cnt;
	}
	else return ans[u][num] = dfs(v,nex,!st + cnt);
	
} 
void solve(){
	int n;
	cin>>n;
	for(int i=1;i<=n;i++){
		cin>>d[i];
		for(int j=0;j<d[i];j++){
			cin>>e[i][j];
		}		
	}
	for(int i=1;i<=n;i++){
		if(!ans[i][0]){
			mp.clear();
			dfs(i,0,0);
		}
		cout<<ans[i][0]<<endl;
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
## L
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define ll long long
#define int long long 
#define lowbit(x) ((x)&(-x))
const int N=2e5+7;
int tri[N<<1],a[N],qs;
vector<int>all;
pair<int,int>id[N];
void add(int idx,int k){//向上更新父节点
    for(int i=idx;i<=all.size();i+=lowbit(i))tri[i]+=k;
}
int sum(int idx){//向下累加子节点
    int tot=0;
    for(int i=idx;i;i-=lowbit(i))tot+=tri[i];
    return tot;
}
int bs(int k){//查找
    int pos=0,mxn=1<<20;
    for(int i=mxn;i>0;i>>=1){
       if(pos+i<=all.size()&&tri[pos+i]<=k){
        pos+=i;  k-=tri[pos];
       } 
    }
    return pos;
}
void solve(){
    int n,q;
    all.clear();
    cin>>n>>q; qs=n-(n/2);
    for(int i=1;i<=n;++i)cin>>a[i],all.emplace_back(a[i]);
    for(int i=1;i<=q;++i){
        cin>>id[i].first>>id[i].second;
        a[id[i].first]+=id[i].second;
        all.emplace_back(a[id[i].first]);
    }
    for(int i=1;i<=q;++i)a[id[i].first]-=id[i].second;
    sort(all.begin(),all.end());
    all.erase(unique(all.begin(),all.end()),all.end());//去重
    fill(tri+1,tri+all.size()+2,0);
    for(int i=1;i<=n;++i){
        int idx=lower_bound(all.begin(),all.end(),a[i])-all.begin()+1;
        add(idx,1);
    }
    for(int i=1;i<=q;++i){
        int p=id[i].first,v=id[i].second;
        int idx=lower_bound(all.begin(),all.end(),a[p])-all.begin()+1;
        add(idx,-1);
        a[p]+=v;
        int new_idx=lower_bound(all.begin(),all.end(),a[p])-all.begin()+1;
        add(new_idx,1);
        cout<<sum(bs(qs))<<endl;
    }
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    cin>>T;
    while(T--)solve();
    return 0;
}


```