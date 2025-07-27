# [831. KMP字符串 AcWing](https://www.acwing.com/problem/content/833/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
#define ll long long
const int N = 1e6+7;
int ne[N],cnt[N];
void solve(){
	int n,m,k=0;
    string p,s;
    cin>>n>>p>>m>>s;
    for(int i=2,j=0;i<p.size()+1;++i){//当我们处理模式串 p 的第 i-1 个字符（0-based）时，实际上是在计算 ne[i] 的值
        while(j&&p[i-1]!=p[j])j=ne[j];
        if(p[i-1]==p[j])++j;
        ne[i]=j;
    }
    for(int i=0,j=0;i<s.size();++i){
        while(j&&s[i]!=p[j])j=ne[j];
        if(s[i]==p[j])j++;
        if(j==p.size())//j的含义是当前已经成功匹配的模式串长度，而不是 “当前匹配到的模式串索引”
            cnt[++k]=i-j+1;
    }
    for(int i=1;i<=k;++i)cout<<cnt[i]<<" \n"[i==k];
}
signed main(){
	ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
   // cin>>T;
	while(T--)solve(); 
	return 0;
}
```