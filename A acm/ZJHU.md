
[P2523 - 零钱兑换 Ⅳ - ZJHUOJ](http://172.20.8.83/problem.php?id=2523)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int mxm=1e2+5,mxn=1e4+5,mod=1e9+7;
int n,m,t,dp[mxm][mxn],k[mxm];
signed main(){
    scanf("%lld",&n);
    for(int i=1;i<=n;++i)scanf("%lld",k+i);
    for(int i=0;i<=n;++i)dp[i][0]=1;
    for(int i=1;i<=n;++i){
        for(int j=1;j<mxn;++j){
            dp[i][j]=dp[i-1][j];
            if(j>=k[i])dp[i][j]=(dp[i][j]+dp[i][j-k[i]])%mod;
        }
    }
 scanf("%lld",&t);
 while(t--){
    scanf("%lld",&m);
    printf("%lld\n",dp[n][m]);
 }
 return 0;
}
```
[P1125 - 种树 Ⅳ - ZJHUOJ](http://172.20.8.83/problem.php?id=1125)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e6+7,inf=0xc0c0c0c0;
int dp[mxn][15],n,m,k,a[mxn];
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    cin>>n>>m>>k;
    for(int i=1;i<=n;++i)cin>>a[i];
    memset(dp,inf,sizeof dp);
    dp[0][0]=dp[1][0]=0,dp[1][1]=a[1];
    for(int i=2;i<=n;++i){
        dp[i][0]=0;
        for(int j=1;j<=m;++j){
            if(i==k)dp[i][j]=dp[i-1][j];
            else dp[i][j]=max(dp[i-1][j],dp[i-2][j-1]+a[i]);
        }
    }
    cout<<dp[n][m]<<endl;
    return 0;
}
```
[P1096 - 2^K区间最大值 - ZJHUOJ](http://172.20.8.83/problem.php?id=1096)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e5+5;
int dp[mxn][20];
signed main(){
    int n,k,b,q;
    scanf("%d%d%d",&n,&k,&q);
    for(int i=1;i<=n;++i)scanf("%d",&dp[i][0]);
    //st表
        for(int j=1;j<=k;++j){//区间2^k个
            for(int i=1;i+(1<<j)-1<=n;++i){
            dp[i][j]=max(dp[i][j-1],dp[i+(1<<j-1)][j-1]);//两个子区间中的最大值
            }
        }
    while(q--){
        scanf("%d",&b);
        printf("%d\n",dp[b][k]);
    }
    return 0;
}
```
[P1068 - 最大和区间 Ⅱ - ZJHUOJ](http://172.20.8.83/problem.php?id=1068)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e4+5,inf=0xc0c0c0c0;
int a[mxn],d[mxn],n,l,r,p,mx;
signed main(){
while(scanf("%d",&n)==1&&n){
    mx=inf,p=l=r=0;
for(int i=1;i<=n;++i){ 
    scanf("%d",a+i);
    d[i]=d[i-1]+a[i];
    if(mx<d[i]-d[p])mx=d[i]-d[p],l=p+1,r=i;  
    if(d[i]-d[p]<0)p=i;//区间和为负舍弃
    }
    if(mx<0)mx=0,l=1,r=n;
    printf("%d %d %d\n",mx,a[l],a[r]);
}
return 0;
}
```
#### 状态机
[P1825 - Children’s Queue - ZJHUOJ](http://172.20.8.83/problem.php?id=1825)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e6+7,mod=1e9+7;
long long int dp[mxn][3];
int n;
signed main(){
    dp[1][0]=dp[1][2]=1;//一个F可能合法为1
    for(int i=2;i<=mxn;++i){
        dp[i][0]=(dp[i-1][1]+dp[i-1][0])%mod;
        dp[i][1]=(dp[i-1][1]+dp[i-1][2])%mod;
        dp[i][2]=dp[i-1][0]%mod;
    }
  while(scanf("%d",&n)==1)printf("%lld\n",(dp[n][0]+dp[n][1])%mod);
 return 0;
}
```
[P1108 - 买卖股票的最佳时机 V - ZJHUOJ](http://172.20.8.83/problem.php?id=1108)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e5+7;
int dp[mxn][5],n,p[mxn];//持股，买，卖，空（不冻），冻结
signed main(){
  ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
  cin>>n;
  for(int i=1;i<=n;++i)cin>>p[i];
  memset(dp,0xc0,sizeof dp);
  dp[1][1]=dp[1][0]=-p[1];dp[1][3]=0;
  for(int i=2;i<=n;++i){
    dp[i][1]=max(dp[i-1][3]-p[i],dp[i-1][4]-p[i]);
    dp[i][0]=max(dp[i-1][1],dp[i-1][0]);
    dp[i][2]=max(dp[i-1][0]+p[i],dp[i-1][1]+p[i]);
    dp[i][4]=dp[i-1][2];
    dp[i][3]=max(dp[i-1][4],dp[i-1][3]);
  }
  cout<<max({dp[n][3],dp[n][4],dp[n][2]})<<endl;
  return 0;
}
```
[P1123 - 母牛的故事 Ⅴ - ZJHUOJ](http://172.20.8.83/problem.php?id=1123)
==状态机--具有周期性的特点==
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e6+7,mod=1e9+7;
long long int dp[mxn][7];
signed main(){
  int t,n;
  dp[1][3]=1;
 for(int i=2;i<mxn;++i){  
     dp[i][4]=(dp[i-1][3]+dp[i-1][6])%mod;
     dp[i][5]=dp[i-1][4];
     dp[i][6]=dp[i-1][5];     
     dp[i][1]=(dp[i][4]+2*dp[i][5]+3*dp[i][6])%mod;
     dp[i][2]=dp[i-1][1];
     dp[i][3]=dp[i-1][2];  
   } 
   scanf("%d",&t);
  while(t--){
    scanf("%d",&n);
    printf("%lld\n",(dp[n][1]+dp[n][2]+dp[n][3]+dp[n][4]+dp[n][5]+dp[n][6])%mod);
  }
  return 0;
}
```
#### 背包
### [Contest1132 - 算法基础——动态规划基础【背包】20240310 - ZJHUOJ](http://172.20.8.83/contest.php?cid=1132)
#### BFS
==结构体相当于指针类型的，当在队列中引用结构体时，修改了一个结构体中的内容，其他的也会跟着变==
[P2795 - 走迷宫 - ZJHUOJ](http://172.20.8.83/problem.php?id=2795)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e2+2;
int dp[mxn][mxn],n,m;
int vis[mxn][mxn];
int dx[] = {1, 0, -1, 0};
int dy[] = {0, -1, 0, 1};
struct road{int x;int y;};
void bfs(){
	road now;
	queue<road>q;
	now.x=now.y=1;
	q.push(now);
	while(!q.empty()){
	    road now=q.front();	
		q.pop();
		if(now.x==n&&now.y==m){
		printf("%d\n",vis[n][m]);
		return;
	}
        for(int i=0;i<4;++i){		
			int x=now.x+dx[i];
			int y=now.y+dy[i];
			if(x<1||y<1||x>n||y>m)continue;
			if(dp[x][y]!=1&&vis[x][y]==0){	
				road nex;	
				nex.x=x;nex.y=y;		
				vis[nex.x][nex.y]=vis[now.x][now.y]+1;
				q.push(nex);
			}			
		}	
	}
	return;
}
signed main(){
	scanf("%d%d",&n,&m);
	for(int i=1;i<=n;++i)for(int j=1;j<=m;++j)scanf("%d",dp[i]+j);
	bfs();
	return 0;
}
```
#### 线性筛
### [素数筛.pdf](http://172.20.8.83/upload/172.20.8.83/20240303/20240303140843_61702.pdf)
[P1879 - 阶乘约数 Ⅱ - ZJHUOJ](http://172.20.8.83/problem.php?id=1879)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int mxn=1e6+7,mod=1e9+7;
int vis[mxn],pri[mxn],tot,n;
void Eulr(int n){
  for(int i=2;i<=n;++i){
    if(!vis[i])pri[++tot]=i;
    for(int j=1;j<=tot;++j){
      if(1LL*i*pri[j]>n)break;
      vis[i*pri[j]]=1;
      if(i%pri[j]==0)break;
    }
  }
}
signed main(){
  scanf("%d",&n);
  Eulr(n);
  long long int t=1;
for(int i=1;i<=tot;++i){
  int m=n,ans=0;
  while(m>=pri[i]){//n!中质因子的个数
    ans+=m/pri[i];//至少贡献一个质因子p
    m/=pri[i];//p^2及更高次幂的贡献
  }
  t=(t*(ans+1))%mod;
}
printf("%lld\n",t);
return 0;
}```
# [9 Divisors](https://www.luogu.com.cn/problem/AT_abc383_d)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int mxn=1e6+7;//由p^2*q^2，根号n就行
int n,vis[mxn],pri[mxn],tot,ans;
void Eulr(){
	for(int i=2;i<mxn;++i){
		if(!vis[i])pri[++tot]=i;
		for(int j=1;pri[j]*i<mxn;++j){//这里的问题
			vis[i*pri[j]]=1;
			if(i%pri[j]==0)break;
		}
	}
}
signed main(){
  ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    cin>>n;
    Eulr();//p^8||p^2*q^2  (8+1)||(2+1)(2+1)
    for(int i =1;i<=tot;++i){
        if(pri[i]*pri[i]*pri[i]*pri[i]>n)break;//i<j总的break;
        if(pri[i]<=100&&pri[i]*pri[i]*pri[i]*pri[i]*pri[i]*pri[i]*pri[i]*pri[i]<=n){
            ++ans;
        }//用这些素数（质因子）能凑成比n小的数
        for(int j=i+1;j<=tot;j++){
            if(pri[i]*pri[i]*pri[j]*pri[j]<=n){
                ++ans;
            }
           else break;//same with first break大了就没必要找了
        }
    }
    cout<<ans;
	return 0;
}//ac的
```
# [选数异或 ](https://www.luogu.com.cn/problem/P8773)
```cpp
注意复习逆元
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
//#define ll long long
const int mxn = 1e5 + 7;
int n, m, x, f[mxn], a, l, r;
map<int, int>las;
void solve() {
    cin >> n >> m >> x;
    for (int i = 1; i <= n; ++i) {
        cin >> a;
        f[i] = max(f[i - 1], las[a ^ x]);//维护，序列可能是无序的，las最后一个出现的位置,(可能会出现在前面，出先在前面就可以以f[i-1]为准)没有的话就是0；
        las[a] = i;//标记位置
    }
    while (m--) {
        cin >> l >> r;
        if (l <= f[r])cout << "yes" << endl;//由于更新，f[r]不会大于r
        else cout << "no" << endl;
    }
    return;
}
signed main() {
    ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int T = 1;
    //cin << T;
    while (T--) solve();
    return 0;
}
```
