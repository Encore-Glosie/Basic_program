team0242, 714357
https://acm.hdu.edu.cn/contests/contest_list.php
# [1010 中位数](https://acm.hdu.edu.cn/contest/problem?cid=1172&pid=1010)
```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define endl "\n"
//#define ll long long
//const int N=2e3+5;
void solve() {
    int ans=0;
    int n; cin>>n;
    int m=2*n+5;
    vector<int>a(n+1),sum(n+1);
    for(int i=1;i<=n;++i)cin>>a[i];
    for(int i=1;i<=n;++i){
        sum[0]=0;//对于每一个a[i]所在的区间
        for(int j=1;j<=n;++j)
        sum[j]=sum[j-1]+(a[j]>a[i]?1:(a[j]<a[i]?-1:0));
        vector<int>l0(m),r0(m),l1(m),r1(m);

        for(int j=1;j<=i;++j){
            int idx=sum[j-1]+n;
            if(j&1)l1[idx]+=j;
            else l0[idx]+=j;
        }

        for(int j=i;j<=n;++j){
            int idx=sum[j]+n;
            if(j&1)r1[idx]+=j;
            else r0[idx]+=j;
        }

        int t=0;
        for(int j=0;j<m;++j)
            t+=l0[j]*r0[j]+l1[j]*r1[j];

        ans+=t*a[i];
    }
    cout<<ans<<endl;
}
signed main() {
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    cin >> T;
    while (T--)solve();
    return 0;
}

```
# [1009 子序列](https://acm.hdu.edu.cn/contest/problem?cid=1172&pid=1009)
```cpp
#include <bits/stdc++.h>
using namespace std;
//#define int long long
#define endl "\n"
//#define ll long long
//const int N=2e3+5;
void solve() {
    int n; cin>>n;
    vector<int>a(n+1),id(n+1);
    for(int i=1;i<=n;++i)cin>>a[i],id[a[i]]=i;
    if(n==1){cout<<1<<endl;return;}
    int l=n+1,r=0,cur=0,cnt=0,mx=0;
    for(int i=n;i;--i){
        int p=id[i];//较大数的位置
        l=min(l,p); r=max(r,p);
        ++cnt;//记录大值
        cur=r-l-(cnt-1)+2;
        mx=max(mx,cur);
    }
    cout<<mx<<endl;
}
signed main() {
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    cin >> T;
    while (T--)solve();
    return 0;
}

```