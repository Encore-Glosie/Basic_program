```cpp
归并排序（并找逆序）： 归并排序使用分治策略，将数组递归地一分为二，直到每个子数组只包含一个元素。
map<string,int>mp
map在迭代器中才可以用first，second
不然就用mp[i]=s;
map的直接赋值法{
m1["def"] = 2;||
m2.insert({ "abc", 1 });
}
归并排列过程示例
```
![[Pasted image 20250411200333.png]]

```cpp 
从上往下递归，从下往上分解
类似dfs的树，and每归并一层都会更新当前排序，然后被上一层作为排序的依据
```
# 归并排序
 ![[Pasted image 20250411202802.png
# [P5149 会议座位 - 洛谷](https://www.luogu.com.cn/problem/P5149)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
#define ll long long
const int mxn=1e5+7;
int a[mxn],n,b[mxn];//b辅助(临时)数组
ll ans;
string s;
map<string,int>mp;//分治、归并排序
void merge(int l,int r){
     if(r<=l)return;
     int mid=l+(r-l>>1);//1LL
     merge(l,mid); merge(mid+1,r);
     int i=l,j=mid+1,k=l;
    while(i<=mid&&j<=r){//先赋值再++
      if(a[i]<a[j])b[k++]=a[i++];//左右两边较小的排在前面
      else b[k++]=a[j++],ans+=mid-i+1;//要比较的两个子序列都已经排好序//在子序列的每个子序列合并时也已经找好逆序数
    }
    while(i<=mid)b[k++]=a[i++];
    while(j<=r)b[k++]=a[j++];//左右两边剩余没排完的排上去
    for(int i=l;i<=r;++i)a[i]=b[i];//更新原数组的排序
    return;
}
void solve(){
  cin>>n;
  for(int i=1;i<=n;++i){
    cin>>s;
    mp[s]=i;
 // mp.insert({s,i});
  }
  for(int i=1;i<=n;++i){
    cin>>s;
    a[mp[s]]=i;
  }
  merge(1,n);
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
```cpp
相信奇迹的人，本身就和奇迹一样了不起。——笛亚 《星游记》
```
##### next_permutation()用法
```cpp
时间复杂度是O(n!)注意剪枝
#include<bits/stdc++.h>
using namespace std;
signed main(){
  int n,a[10]={1,2,3,4,5};
  do{
   for(int i=0;i<=4;++i)cout<<a[i];
   cout<<endl;
  }while(next_permutation(a,a+5));//最好用一个数组来存数
  return 0;
}
注：next_permutation()函数从当前的全排列开始，逐个输出更大的去安排列，而不是输出所有的全排列
如果想要得到全排列可以先用sort排序
```
==要对杨辉三角数敏感==
##### 杨辉三角代码
（now number=同列上一层的前两个数字相加）
```cpp
c[1][1]=1;//最左上角的数初始化为1 
for(int i=2;i<=n;i++)
for(int j=1;j<=i;j++) c[i][j]=c[i-1][j]+c[i-1][j-1];//每个数都等于它肩上两数之和
法二
//下面构造杨辉三角(即组合数表)
pc[0]=pc[n-1]=1; //从0开始，杨辉三角性质,两边都是1 
if (n>1)for(int i=1;i*2<n;i++)
pc[i]=pc[n-1-i]=(n-i)*pc[i-1]/i; //利用杨辉三角对称性和组合数公式计算
```
### [P1118 Backward Digit Sums G/S - 洛谷](https://www.luogu.com.cn/problem/P1118)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//#define Ll unsigned long long
//const int mxn=3e5+7;
//string s;
int n,m,t,a[20],b[20][20];
void solve(){
  cin>>n>>m;
  a[1]=1, b[1][1]=1;//最后一行各系数恰好是杨辉三角数！
 for(int i=2;i<=n;++i){//第i层，杨辉三角是从1开始的
  a[i]=i;
 for(int j=1;j<=i;++j)b[i][j]=b[i-1][j]+b[i-1][j-1];}
 do{
  t=0;
  for(int i=1;i<=n;++i){
     t+=a[i]*b[n][i];
    if(t>m)break;
  }
  if(t==m){
    for(int i=1;i<=n;++i)cout<<a[i]<<(i==n?"\n":" ");
    break;
    }
 }while(next_permutation(a+1,a+1+n));
  return ;
}
signed main(){
  ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
   int T=1;
  //cin>>T;
  while(T--)solve();
  return 0;
}
代码2
int n,m,a[20],b[20][20],vis[20];
void dfs(int k,int t){//t要放在这里,不然会一直被加
  if(t>m)return;
  if(k==n+1&&t==m){
    for(int i=1;i<=n;++i)cout<<a[i]<<(i==n?"\n":" ");
   exit(0) ;//正常运行并退出程序
  }
   if(k==n+1)return;
  for(int i=1;i<=n;++i){
    if(!vis[i]){
       vis[i]=1;//在for循环里标记！
      a[k]=i;
       dfs(k+1,t+i*b[n][k]);
     vis[i]=0;//每次dfs完赶紧复位！return后把vis变成0供下一次根节点搜索的使用
      }
  }
}
void solve(){
  cin>>n>>m;
  b[1][1]=1;
  for(int i=2;i<=n;++i)
    for(int j=1;j<=i;++j)
    b[i][j]=b[i-1][j-1]+b[i-1][j];
  dfs(1,0);
  return ;
}

```
# [方格取数 - 洛谷](https://www.luogu.com.cn/problem/P1004)
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
const int mxn=20;
int dp[mxn][mxn][mxn],a[mxn][mxn],w[mxn][mxn],n,m,ans;
// int read(){
//   int x=0; bool t=false; char ch=getchar();
//   while((ch<'0'||ch>'9')&&ch!='-')ch=getchar();
//   if(ch=='-')t=true, ch=getchar();
//   while(ch<='9'&&ch>'0')x=x*10+ch-48,ch=getchar();
//   return t? -x:x; 
// }//快读
void solve(){
cin>>n;
int a,b,c;
while(cin>>a>>b>>c,a|b|c){
  w[a][b]=c;
 // cout<<w[a][b]<<endl;
}
int x2,y2;
for(int k=2;k<=2*n;++k){//k<=2*n是因为省略了纵坐标循环，实际上至少走2*(n-1)步才能到达
for(int x1=1;x1<=n;++x1){
    for(int x2=1;x2<=n;++x2){
      int y1=k-x1,y2=k-x2;
      int t=w[x1][y1];
      if(x1!=x2)t+=w[x2][y2];
      int &x=dp[k][x1][x2];
      x=max(x,dp[k-1][x1-1][x2]+t);
      x=max(x,dp[k-1][x1-1][x2-1]+t);//dd x是由上一步继承来的，y是现在的位置，则表示的位移是dd
      x=max(x,dp[k-1][x1][x2-1]+t);
      x=max(x,dp[k-1][x1][x2]+t);//rr
      //在x1,x2的移动一步中选择最大的那个，这一步状态是由上一步得来的
    }
   }
  }
  cout<<dp[2*n][n][n]<<endl;
}
signed main(){
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T = 1;
	//cin >> T;
	while (T--)solve();
	return 0;
}
```
