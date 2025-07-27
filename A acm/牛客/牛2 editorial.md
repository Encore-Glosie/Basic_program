## A
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int N=5e5+7,mod=998244353;
int s[N],sum[N]={1};
void solve(){
	int n,ans=0,cnt=0;
	cin>>n;
	for(int i=1;i<=n;i++) cin>>s[i], cnt+=(s[i]==-1);
	for(int i=1;i<=n;i++){//只看(能)新增加的1
		if(s[i]==1&&s[i-1]==0) ans=(ans+sum[cnt])%mod;//01
		else if(s[i]==1&&s[i-1]==-1) ans=(ans+sum[cnt-1])%mod;
		else if(s[i]==-1&&s[i-1]==0) ans=(ans+sum[cnt-1])%mod;
		else if(s[i]==-1&&s[i-1]==-1) ans=(ans+sum[cnt-2])%mod;
	}
	cout<<ans%mod<<endl;
	return ;
}
signed main(){
	ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
	for(int i=1;i<N;i++) sum[i]=(sum[i-1]<<1)%mod;
	int T=1;
    cin>>T;
    while(T--)solve();
	return 0;
}


```