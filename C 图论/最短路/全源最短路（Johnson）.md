
# [P5905 【模板】全源最短路（Johnson） - 洛谷](https://www.luogu.com.cn/problem/P5905)

```cpp
Johnson 算法
强制连通全图，解决 初始源点无法覆盖所有节点
全源最短路是计算图中所有节点对之间的最短路径。
单源最短路是指从一个起点出发，计算到所有其他节点的最短路径。
全源最短路由于点之间可能不连通要所以检查从每一个节点为起点的路径上的负环，这时候就可以用spfa(0)是全源连通的情况下找
单源最短路判断负环一般仅是求从一个起点的路径上的最短路及负环，因为某个最短路上要是有负环，则这个最短路无意义

#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
#define ll long long
const int inf = 1e9,INF=0x3f3f3f3f;
const int N = 3e3 + 5, M = 1e4 + 5;//加边了，M要扩大！
int e[M], h[N], ne[M], st[N], dist[N], dish[N], cnt[N], w[M], idx, n, m, f;
ll ans;
typedef pair<int, int> PII;

void add(int a, int b, int c) {
    w[idx] = c;
  //  original_w[idx] = c;  // 保存原始边权
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}
int spfa() {  // 超级源点的作用：强制连通
    memset(dish, INF, sizeof dish);//按位填充，这里不能直接用1e9!!!
    dish[0] = 0; 
    cnt[0] = 1;   
    queue<int> q;
    q.push(0);
    st[0] = 1;
    while (!q.empty()) {
        int t = q.front();
        q.pop();
        st[t] = 0;
        for (int i = h[t]; i != -1; i = ne[i]) {
            int j = e[i];
            if (dish[j] > dish[t] + w[i]) {
                dish[j] = dish[t] + w[i];
                if (!st[j]) {
                    ++cnt[j];
                    if (cnt[j] > n) return 1;  // 存在负环
                    st[j] = 1;
                    q.push(j);
                }
            }
        }
    }
    return 0;
}

void Dijkstra(int u) {
    for (int i = 1; i <= n; ++i) 
        dist[i] = inf;
        memset(st,0,sizeof st);
    dist[u] = 0;
    priority_queue<PII, vector<PII>, greater<PII>> heap;
    heap.push({0, u});
    while (!heap.empty()) {
        PII t = heap.top();
        heap.pop();
        int ver = t.second;
        if (st[ver]) continue;
        st[ver] = 1;
        for (int i = h[ver]; i != -1; i = ne[i]) {
            int j = e[i];
            if (dist[j] > dist[ver] + w[i]) {
                dist[j] = dist[ver] + w[i];
                heap.push({dist[j], j});
            }
        }
    }
}

void solve() {
    memset(h, -1, sizeof h);  
    int a, b, c;
    cin >> n >> m;
    while (m--) {
        cin >> a >> b >> c;
        add(a, b, c);
    }

    for (int i = 1; i <= n; ++i) add(0, i, 0);//这里又加边了，idx++,M要更大
    
    if (spfa()) { cout << -1 << endl; return; }
    
    for (int i = 1; i <= n; ++i) 
        for (int j = h[i]; j != -1; j = ne[j]) 
            w[j] = w[j] + dish[i] - dish[e[j]];
    
    // 对每个节点运行Dijkstra
    for (int i = 1; i <= n; ++i) {
        Dijkstra(i);
        ans = 0; 
        for (int j = 1; j <= n; ++j) {
            if (dist[j] == inf) ans +=  (ll)inf * j;//要加ll防止溢出 
            else ans += (ll)j * (dist[j] + dish[j] - dish[i]);
        }
        cout << ans << endl;
    }
}
signed main() {
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T = 1;
    //cin >> T;
    while (T--) solve();
    return 0;
}   
```