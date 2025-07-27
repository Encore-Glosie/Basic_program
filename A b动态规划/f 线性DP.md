
### LIA:
![[Pasted image 20250509202837.png]]
```cpp
可惜了，要是该题是将已给序列恢复原序列，则可以用LCIS(最长连续递增(非单调)子序列)!
//理解写法 O(n) 容易超时
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
void solve(){
 int n; cin >> n;
 vector <int> a(n),b(n,1);
 for(auto &x: a) cin >> x;
 int mx=1;//LIA
 for(int i=1; i<n; ++i){
	for(int j=0; j<i; ++j)
	if(a[i]>a[j])b[i]=max(b[i],b[j]+1);
	mx = max(mx, b[i]);
 }
 cout << n-mx <<endl;;
 }
signed main(){
	ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
	int T = 1;
	cin >> T; 
	while( T-- ) solve();
	return 0;
}
优化：
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
void solve(){
 int n; cin >> n;
 vector <int> a(n+1), p(n+1);
 for(int i=1; i<=n; ++i) cin >> a[i], p[a[i]]=i;
 int mx=1, cur=1;//LIA
 for(int i=2; i<=n; ++i){
    if(p[i] > p[i-1]) ++cur, mx=max(mx,cur);
	else cur=1;
 }
 cout << n-mx <<endl;;
 }
signed main(){
	ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
	int T = 1;
	cin >> T; 
	while(T--) solve();
	return 0;
}
```
# [896. 最长上升子序列 II - AcWing题库](https://www.acwing.com/problem/content/898/)
辨析：[Problem - 847B - Codeforces](https://codeforces.com/problemset/problem/847/B)
O(n^2)做法
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//vector<pair<int,int>>E[mxn];
//double ans=DBL_MAX;//double的最大值
//vector<vector<int>>e(mxn);
const int mxn=1e3+7;
int a[mxn],n,f[mxn],ans;
void solve(){
 cin>>n;
 for(int i=1; i <= n; ++i)cin >> a[i];
 for(int i = 1; i <= n; ++ i){
  f[i]=1;
  for(int j =1; j < i; ++ j){
    if(a[i] > a[j]) f[i] = max(f[i], f[j]+1);
  }
 }
  for(int i=1; i <= n; ++i)ans=max(ans, f[i]);
 cout << ans << endl;
}
signed main(){
  ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
   int T=1;
  //cin>>T;
  while(T--)solve();
  return 0;
}

```
O(n * logn)做法：
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define ll long long
const int N = 2e5 + 7;
const int inf=0xc0c0c0c0;
//LIS
int a[N],last[N]={inf},cnt;
vector<int>ans[N];
void solve(){
    int n,cnt=0; cin >> n;
   for(int i=1;i<=n;++i)cin>>a[i];
   for(int i=1;i<=n;++i){
    if(a[i]>last[cnt]){
      last[++cnt]=a[i];//维护最大上升子序列的最大值
     // ans[cnt].push_back(a[i]);
    }//大于直接插入，小于找到一个正好大于的地方更新
    else{
      int l=0,r=cnt;
      while(l<r){
        int mid=l+r>>1;
        if(a[i]<=last[mid])r=mid;//找到第一个LIS
        else l=mid+1;
      }
      //ans[l].push_back(a[i]);
      last[l]=a[i];//更新
    }
   }
//    for(int i=1;i<=cnt;++i){
//     for(auto &x:ans[i])cout<<x<<" ";
//    cout<<endl;
//    }
cout<<cnt<<endl;
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
错误的代码：

#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define ll long long
const int N = 2e5 + 7;
const int inf=0xc0c0c0c0;
//LIS
int a[N],last[N]={inf},cnt;
//vector<int>ans[N];
void solve(){
    int n,cnt=0; cin >> n;
   for(int i=1;i<=n;++i)cin>>a[i];
   for(int i=1;i<=n;++i){
    if(a[i]>last[cnt]){
      last[++cnt]=a[i];
    }//大于直接插入，小于找到一个正好大于的地方更新
    else{
      int l=0,r=cnt;
      while(l<r){
        int mid=l+r>>1;
        if(last[mid]>=a[i])r=mid;
        else l=mid+1;
      }
      last[l]=a[i];//更新使此长度上升自序列的末尾值最小
    }
   }
   cout<<cnt<<endl;
   for(int i=1;i<=cnt;++i)cout<<last[i]<<" \n"[i==cnt];
}

signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}
```
## last无法正确输出LIS
因为每次更新会把后面的最小值替换到前面去，也可以说last之间是独立的，它的任务是维持与cnt有关的最小值

|     |      |         |                    |     |
| --- | ---- | ------- | ------------------ | --- |
| i   | a[i] | 操作      | last 数组更新          | cnt |
| 1   | 3    | 放入空尾    | last = [3]         | 1   |
| 2   | 10   | 10 > 3  | last = [3, 10]     | 2   |
| 3   | 2    | 替换 3    | last = [2, 10]     | 2   |
| 4   | 1    | 替换 2    | last = [1, 10]     | 2   |
| 5   | 20   | 20 > 10 | last = [1, 10, 20] | 3   |
# [897. 最长公共子序列 - AcWing题库](https://www.acwing.com/problem/content/899/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//#define ULL unsigned long long
//const int N=1e5+3,P=131;
const int N=1e3+10,M=N*31;
//ai,bj不相等的话会继承上一个其中一个的最大值；
//相等的话会在继承的最大值的基础上+1
//遍历两次即可找到最大值
int f[N][N];
char a[N],b[N];
void solve(){
   int n,m;
   cin>>n>>m>>a+1>>b+1;
   for(int i=1;i<=n;++i){
    for(int j=1;j<=m;++j){
        if(a[i]==b[j])f[i][j]=max(f[i][j],f[i-1][j-1]+1);
        else f[i][j]=max(f[i-1][j],f[i][j-1]);
    }
   }
    cout<<f[n][m]<<endl;
}  
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
   while(T--)solve();
   return 0;
}

```
# [902. 最短编辑距离 - AcWing题库](https://www.acwing.com/problem/content/904/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
#define ll long long
const int N = 1e3+7;
int f[N][N];
char a[N],b[N];
void solve(){
int n,m; cin>>n>>a+1>>m>>b+1;
for(int i=1;i<=n;++i)f[i][0]=i;
for(int i=1;i<=m;++i)f[0][i]=i;
for(int i=1;i<=n;++i){
    for(int j=1;j<=m;++j){
        if(a[i] == b[j])f[i][j] = f[i-1][j-1];  // 直接继承
        else f[i][j] = min({f[i-1][j], f[i][j-1], f[i-1][j-1]}) + 1;
    }
}
cout<<f[n][m]<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}

```
# [899. 编辑距离 - AcWing题库](https://www.acwing.com/problem/content/901/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
#define ll long long
const int N = 2e3+7;
int f[N][N];
string s[N];
int n;
int check(string s2,string s3){
    int la=s2.size(),lb=s3.size();
    s2=' '+s2; s3=' '+s3;
    for(int i=1;i<=la;++i)f[i][0]=i;
    for(int i=1;i<=lb;++i)f[0][i]=i;
    for(int i=1;i<=la;++i){
        for(int j=1;j<=lb;++j){
            if(s2[i]==s3[j])f[i][j]=f[i-1][j-1];
            else f[i][j]=min({f[i-1][j],f[i][j-1],f[i-1][j-1]})+1;//删除a[i]，插入b[j]，替换
        }
    }
return f[la][lb];
}
void solve(){
int n,m;
 cin>>n>>m;
 for(int i=1;i<=n;++i)cin>>s[i];
 while(m--){
    string s1;
    int li,res=0;
    cin>>s1>>li;
    for(int i=1;i<=n;++i)
        if(check(s[i],s1)<=li)++res;
         cout<<res<<endl;
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