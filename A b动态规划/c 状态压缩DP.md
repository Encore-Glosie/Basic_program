![[Pasted image 20250725213409.png]]
![[Pasted image 20250725215815.png]]


-- 外层的 `for (int i = 1; i <= m; i++)` 是在 **按列从左到右逐列枚举**
- 中间的 `j` 是在 **枚举这一列（第 i 列）的所有 2ⁿ 种状态**
- 内层的 `k` 是在 **尝试用前一列（第 i-1 列）的状态 `k`，转移到这一列状态 `j`
- 若j和k即第i和i-1行满足合并的条件则 += 即可以合并到i上

-一共有n行，把每个格子看成而进制，则每个列是一个二进制数，每一列的每一格都对应一个1或0 两种状态，在i的下计情况算整个列的状态

因为当你表示一个 `n` 位的二进制数时，合法的范围是：
`0 ~ (1<<n) - 1`
也就是总共有 `2^n` 种状态。

# [291. 蒙德里安的梦想 - AcWing题库](https://www.acwing.com/problem/content/293/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
#define ll long long
const int N=12,M=1<<N;
bool st[M];
ll f[N][M];
void solve(){
    int n,m,cnt;
    while(cin>>n>>m,n||m){

        for(int i=0;i<(1<<n);++i){
            st[i]=1;cnt=0;
            for(int j=0;j<n;++j){
                if((i>>j)&1){
                    if(cnt&1){//连续的0断了
                        st[i]=false;
                        break;
                        }
                }
                else ++cnt;
            }
            if(cnt&1)st[i]=false;//处理高位的0
        }

        memset(f,0,sizeof f);
        f[0][0]=1;
        for(int i=1;i<=m;++i)
            for(int j=0;j<(1<<n);++j)
                for(int k=0;k<(1<<n);++k)//不出现重叠的1且不出现奇数个0
                    if((j&k)==0&&(st[j|k]))f[i][j]+=f[i-1][k];
        cout<<f[m][0]<<endl;//第m列不横放即为答案
    }
}
int main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}
```
# [91. 最短Hamilton路径 - AcWing题库](https://www.acwing.com/problem/content/93/)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
#define ll long long
const int N=20,M=1<<N;
//bool st[M];
int w[N][N];
ll f[M][N];
void solve(){
   int n; cin>>n;
   for(int i=0;i<n;++i)
        for(int j=0;j<n;++j)cin>>w[i][j];
    memset(f,0x3f,sizeof f);
    f[1][0]=0;
    for(int i=0;i<1<<n;++i){
        for(int j=0;j<n;++j){
            if((i>>j)&1)for(int k=0;k<n;++k)
                if((i>>k)&1)f[i][j]=min(f[i][j],f[i-(1<<j)][k]+w[k][j]);
        }                              //i-j, last(i)->k-j
    }
    cout<<f[(1<<n)-1][n-1]<<endl;//位运算的优先级低于'+'-'
}
int main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}
```