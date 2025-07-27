# Trie字符串统计
# Trie(01)字典树

我们想要的是 **两个数异或的最大值**。为了获得最大异或值，我们需要：
- **尽量使每一位异或的结果为 `1`**，也就是说：
    - 如果当前位是 0，希望找一个 1；
    - 如果当前位是 1，希望找一个 0；
这正是 **Trie（01 字典树）+ 贪心匹配** 的完美应用场景。

# [835. Trie字符串统计 - AcWing题库](https://www.acwing.com/problem/content/837/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
const int N=1e5+7;
int son[N][27],cnt[N],idx;
void insert(string s){
    int p=0;//从0开始往下延伸，即0为根节点
    for(int i=0;i<s.size();++i){
        int u=s[i]-'a';
        if(!son[p][u])son[p][u]=++idx;
        p=son[p][u];
    }
    ++cnt[p];
}
int query(string s){
    int p=0;
    for(int i=0;i<s.size();++i){
        int u=s[i]-'a';
        if(!son[p][u])return 0;
        p=son[p][u];//都是最终遍历到p节点
    }
    return cnt[p];
}
void solve(){
    int n;  cin>>n;
    string s;
    char q;
    while(n--){
        cin>>q>>s;
        if(q=='I')insert(s);
        else cout<<query(s)<<endl;
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

# [143. 最大异或对 - AcWing题库](https://www.acwing.com/problem/content/145/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
//#define int long long
//#define ll long long
//#define ULL unsigned long long
//const int N=1e5+3,P=131;
const int N=1e5+10,M=N*31;
int a[N],son[M][2],n,idx;
void insert(int x){
    int p=0;
    for(int i=30;i>=0;--i){
        int u=x>>i&1;
        if(!son[p][u])son[p][u]=++idx;//根节点为0 
        p=son[p][u];
    }
}
int query(int x){
    int p=0,res=0;
    for(int i=30;i>=0;--i){
        int u=x>>i&1;
        if(son[p][!u]){
            p=son[p][!u];
            res=(res<<1)+!u;//位运算最后要
        }
        else{
            p=son[p][u];
            res=(res<<1)+u;
        }
    }
    return res;
}
void solve(){
    cin>>n;
    for(int i=0;i<n;++i)cin>>a[i];
    int res=0;
    for(int i=0;i<n;++i){
        insert(a[i]);
        int t=query(a[i]);
        res=max(res,a[i]^t);
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


