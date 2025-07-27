# [D - Line Crossing](https://atcoder.jp/contests/abc402/tasks/abc402_d)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define int long long
//#define ll long long
//#define Ll unsigned long long
//const int mxn=2e6+7;
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
// vector<int>st[mxn];//都是二维容器
// vector<int>cnt(mxn);//数组
int n,m,t,b,f,a,ans,k;
void solve(){
  //1st:n个点，且任意三点不共线，最多有n*(n-1)/2条线(两两)相交;
  //2nd:N个点等分圆，若任意两对点满足(a+b)%N,则则两对点对应的直线平行;
  //3th:如果有k条斜率相同的直线，那么就有k*(k−1)/2对平行线;
   cin>>n>>m;
   vector<int>cnt(n);//vector在局部的初始值也是0；
   for(int i=1;i<=m;++i){
    cin>>a>>b;
    ++cnt[(a+b)%n];
   }
    t=(m*(m-1))/2LL;
  for(auto it:cnt)
    t-=it*(it-1)/2LL;
  cout<<t<<endl;
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