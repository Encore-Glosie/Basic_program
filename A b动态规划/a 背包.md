*01背包VS完全背包（使用一维数组的情况下）：
01背包要求只选一次，体积要从后往前遍历，保证前面的体积没有被当前的数据更新，从而保证了只选一次
完全背包可以重复选多次，体积从前后遍历体现了前面已经选择了若干个

*二维数组都可以从前往后遍历
### 转化成01背包的最重要的就是找到相对应的体积和价值*
# 完全背包
# [3. 完全背包问题 - AcWing题库](https://www.acwing.com/file_system/file/content/whole/index/content/3554/)
特点：每个商品可以选无限个
做法：
1. 错位相减消去k可得状态转移方程
2. 从前往后遍历
```cpp
//理解代码
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
//typedef pair<int, int>PII;
const int mxn=1e3+7;
int v[mxn],w[mxn],f[mxn][mxn],ans,n,m,mxv;
void solve(){
  cin>>n>>m;
  for(int i=1;i<=n;++i)cin>>v[i]>>w[i];
  for(int i=1;i<=n;++i){//product
    for(int j=1;j<=m;++j){//volum
    f[i][j]=f[i-1][j];//不管怎样先把上一个继承来再说，以防把f[i][j]直接continue掉了
    if(v[i]>j)continue;
      for(int k=0;k*v[i]<=j;++k){
        f[i][j]=max(f[i][j],f[i-1][j-k*v[i]]+k*w[i]);
      }
    }
  }
  cout<<f[n][m]<<endl;
}
signed main(){
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T = 1;
	//cin >> T;
	while (T--)solve();
	return 0;
}
//层层优化
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
//typedef pair<int, int>PII;
const int mxn=1e3+7;
int v[mxn],w[mxn],f[mxn][mxn],ans,n,m,mxv;
void solve(){
  cin>>n>>m;
  for(int i=1;i<=n;++i)cin>>v[i]>>w[i];
  for(int i=1;i<=n;++i){//product
    for(int j=0;j<=m;++j){//volum
      f[i][j]=f[i-1][j];//先要继承
      if(j>=v[i])f[i][j]=max(f[i][j],f[i][j-v[i]]+w[i]);//利用公式把k消掉
    }
  }
  cout<<f[n][m]<<endl;
}
signed main(){
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T = 1;
	//cin >> T;
	while (T--)solve();
	return 0;
}

//终极一维解法
#include <bits/stdc++.h>
using namespace std;
const int N = 1010;
int n, m;
int f[N];
// 完全背包问题
int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) {
        int v, w;
        cin >> v >> w;
        for (int j = v; j <= m; j++)
            f[j] = max(f[j], f[j - v] + w);
    }
    printf("%d\n", f[m]);
    return 0;
}
```
![[微信图片_20250429173202 3.jpg]]
# 分组背包
# [9. 分组背包问题 - AcWing题库](https://www.acwing.com/file_system/file/content/whole/index/content/3560/)
特点：每组最多选一个
做法：
1. 总的可选数n等于组数
2. 一维数组从后往前遍历体积，分别遍历组数(个数)，体积，和每种中是否挑选某个
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
//typedef pair<int, int>PII;
const int mxn=1e3+7;
int v[mxn][mxn],w[mxn][mxn],f[mxn][mxn],k[mxn],ans,n,m,mxv;
void solve(){
  cin>>n>>m;
  for(int i=1;i<=n;++i){
    cin>>k[i];
    for(int j=1;j<=k[i];++j)cin>>v[i][j]>>w[i][j];//第i组，第j个
  }
  
  for(int i=1;i<=n;++i){//product
    for(int j=0;j<=m;++j){//volum
    f[i][j]=f[i-1][j];//不选，要在这里继承上一组的值
    for(int r=1;r<=k[i];++r){   
       if(j>=v[i][r])f[i][j]=max(f[i][j],f[i-1][j-v[i][r]]+w[i][r]);
    }
    }
  }
  cout<<f[n][m]<<endl;
}
signed main(){
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T = 1;
	//cin >> T;
	while (T--)solve();
	return 0;
}
//一维数组
 for(int i=1;i<=n;++i){//produc
    for(int j=m;j;--j){//volum
    for(int r=1;r<=k[i];++r){//因为只用到了i-1，所以可以直接到着来，把i-1去掉
       if(j>=v[i][r])f[j]=max(f[j],f[j-v[i][r]]+w[i][r]);//继续上一个状态的装或者这一个状态的不装
    }
   }
  }
  cout<<f[m]<<endl;
```
# 多重背包
特点：有多组物品，每种可选多件
做法：
1. 每次选取的多件看作一个整体，当成01背包来做
# [4. 多重背包问题 I - AcWing题库](https://www.acwing.com/problem/content/4/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
#define ll long long
const int N=1e2+5;
int v[N],w[N],f[N],k[N];
void solve(){
    int n,V,ans=0; cin>>n>>V;
    for(int i=1;i<=n;++i){
        cin>>v[i]>>w[i]>>k[i];
        for(int j=V;j>=v[i];--j){
            for(int c=1;c<=k[i];++c){
               if(j>=c*v[i])f[j]=max(f[j],f[j-c*v[i]]+c*w[i]);
            }
        }
    }
    cout<<f[V]<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}

```

# [5. 多重背包问题 II - AcWing题库](https://www.acwing.com/problem/content/description/5/)
```cpp
二进制优化：
一个正整数n，可以被分解成 1,2,4,…,2^(k-1),n-2^k+1（2的次幂）的形式
这些正整数（相加）可以表示1~n的所有数
（也就是拆分成 1+1+1+1... 然后转成二进制的数）
```
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
//typedef pair<int, int>PII;
const int mxn=2e3+7;
struct st{
  int v;
  int w;
}good;
int f[mxn],k,ans,n,m,v,w,s;
void solve(){
  vector<st>goods;//vector的每一项都是结构体，后面可以用st.v,st.w非常方便
  cin>>n>>m;
  for(int i=1;i<=n;++i){
    cin>>v>>w>>s;
    for(int k=1;k<=s;k*=2){
      s-=k;
      goods.push_back({v*k,w*k});
    }
    if(s>0)goods.push_back({v*s,w*s});
    //把所有的都拆解了，放到vector中了，剩下的就是01背包了，看每项拿不拿
  }  
  for(auto it:goods)
  for(int j=m;j>=it.v;j--)
  f[j]=max(f[j],f[j-it.v]+it.w);
  cout<<f[m]<<endl;
}
signed main(){
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T = 1;
	//cin >> T;
	while (T--)solve();
	return 0;
}

```


## [AcWing 1015. 摘花生 - 糖豆爸爸 - 博客园](https://www.cnblogs.com/littlehb/p/15608068.html)
```cpp
#include <bits/stdc++.h> using namespace std; 
const int N = 110;
int n; int w[N][N], 
f[N][N]; 
int main() { 
for (int i = 1; i <= n; i++) 
for (int j = 1; j <= n; j++) cin >> w[i][j]; 
memset(f, 0x3f, sizeof f);
for (int i = 1; i <= n; i++) 
for (int j = 1; j <= n; j++) {
if (i == 1 && j == 1) f[i][j] = w[i][j]; //特判，比赋初始值好理解
else f[i][j] = max(f[i - 1][j], f[i][j - 1]) + w[i][j];
} 
printf("%d\n", f[n][n]); 
return 0;
}
```
# [AcWing 1027. 方格取数 - 糖豆爸爸 - 博客园](https://www.cnblogs.com/littlehb/p/15637264.html)
==来回路径模板== / ==方格取数模型== / ==三重迭代模型==
```cpp
四维数组可以在100以内，要慎用
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
const int mxn=1e2+7;
// INF=0x3f3f3f3f;
int dp[mxn*2][mxn][mxn], w[mxn][mxn], ans, n,t;
void solve(){
  cin>>n;
  int a,b,c;
  while(cin>>a>>b>>c,a||b||c)w[a][b]=c;
  for(int k=2;k<=2*n;++k)//步调一致，横纵坐标之和,可减少变量的循环
  for(int x1=1;x1<=n;++x1)
  for(int x2=1;x2<=n;++x2){
    int y1=k-x1,y2=k-x2;
   if(y1>0&&y1<=n&&y2>0&&y2<=n){
     t=w[x1][y1];
    if(x1!=x2)t+=w[x2][y2];
      int &x=dp[k][x1][x2];//quote
        x=max(x,dp[k-1][x1-1][x2-1]+t);//dd
        x=max(x,dp[k-1][x1][x2-1]+t);//rd
        x=max(x,dp[k-1][x1][x2]+t);//rr
        x=max(x,dp[k-1][x1-1][x2]+t);//dr  
  }
  }
 cout<<dp[2*n][n][n]<<endl;
}
signed main(){
  ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
   int T=1;
  //cin>>T;
  while(T--)solve();
  return 0;
}
```
![[Pasted image 20250425202855.png]]
[AcWing 187. 导弹防御系统 - 糖豆爸爸 - 博客园](https://www.cnblogs.com/littlehb/p/15654801.html)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
//typedef pair<int, int>PII;
const int mxn = 1e2 + 7;
int a[mxn],up[mxn],down[mxn],n,ans;
void dfs(int st,int su,int sd){
    if(su+sd>=ans)return;
    if(st==n){
      ans=su+sd;
      return;
    }
    //up sub
    int k=0;
    while(k<su&&up[k]>=a[st])k++;
    int t=up[k];
    up[k]=a[st];
    if(k<su)dfs(st+1,su,sd);///上升
    else dfs(st+1,su+1,sd);//否则up[k]中的都大于a[st],非上升，要加系统
    up[k]=t; //回溯还原 
   //down sub
   k=0;
   while(k<sd&&down[k]<=a[st])k++;
    t=down[k];
    down[k]=a[st];
    if(k<sd)dfs(st+1,su,sd);
    else dfs(st+1,su,sd+1);
    down[k]=t;
}
void solve() {
while(cin>>n,n){
  ans=n;
  for(int i=0;i<n;++i)cin>>a[i];
  dfs(0,0,0);
  cout<<ans<<endl;
}
}
signed main() {
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T = 1;
	//cin >> T;
	while (T--)solve();
	return 0;
}
```
![[Pasted image 20250427191320.png]]

*数字三角形可以用这种方式来记录坐标，从上往下的行，从左往右的列*

