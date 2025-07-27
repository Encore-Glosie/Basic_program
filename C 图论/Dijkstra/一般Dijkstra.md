### 条件：不存在负权边
## 朴素版Dijkstra
O(n^2)

## [P2799 - Dijkstra求最短路 I - ZJHUOJ](http://172.20.8.83/problem.php?id=2799)
*稀疏图(==即边与点差不多m<<n^2==)用邻接矩阵来求，稠密图(==即边数远远大于点数m≈n^2==)用邻接表来求*
```cpp
朴素版dijkstra适合稠密图
#include<bits/stdc++.h>
using namespace std;
#define endl '\n'
const int inf=0x3f3f3f3f;
const int N=5e2+5;
int g[N][N];//稠密图用邻接矩阵
int st[N],dist[N],n;
// void add(int a,int b){
//     e[idx]=b, ne[idx]=h[a], h[a]=idx++;
// }
int Dijkstra(){//从起点到所有其他节点的最短路径
    dist[1]=0;
    for(int i=0;i<n;++i){//有n个点所以要进行n次迭代
        int t=-1;
        for(int j=1;j<=n;++j)
            if(!st[j]&&(t==-1||dist[t]>dist[j]))t=j;
            st[t]=1;
        for(int j=1;j<=n;++j)
            dist[j]=min(dist[j],dist[t]+g[t][j]);//更新邻边    
    }
    return (dist[n]==inf?-1:dist[n]);
}
void solve(){
    memset(dist,inf,sizeof dist);
    memset(g,inf,sizeof g);
    int m,a,b,c;
    cin>>n>>m;
    while(m--){
        cin>>a>>b>>c;
        g[a][b]=min(g[a][b],c);//如果发生重边的情况则保留最短的一条边
    }
    cout<<Dijkstra()<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
   // cin>>T;
    while(T--)solve();
    return 0;
}
```
## 堆优化版Dijkstra
O(mlogm)
## [P2800 - Dijkstra求最短路 II - ZJHUOJ](http://172.20.8.83/problem.php?id=2800) 

看一下算法的时间复杂度：
for(i:1 ~ n)//n次
{
    t <- 没有确定最短路径的节点中距离源点最近的点;//每次遍一遍历dist数组，n次的复杂度是O(n^2)
    state[t] = 1;
    更新 dist;//每次遍历一个节点的出边，n次遍历了所有节点的边，复杂度为O(e)
}
算法的主要耗时的步骤是从dist 数组中选出：没有确定最短路径的节点中距离源点最近的点 t。只是找个最小值而已，没有必要每次遍历一遍dist数组。
在一组数中每次能很快的找到最小值，很容易想到使用小根堆。可以使用库中的小根堆（推荐）或者自己编写。

```cpp
代码：

标准版：

#include<bits/stdc++.h>
using namespace std;
#define endl "\n"
const int inf=0x3f3f3f3f;
const int N=1e6+5;
int st[N],e[N],h[N],ne[N],w[N],dist[N],idx,n;
typedef pair<int,int>PII;
void add(int a,int b,int c){
    w[idx]=c;
    e[idx]=b;
    ne[idx]=h[a];
    h[a]=idx++;
}
int Dijkstra(){
    dist[1]=0;
    priority_queue<PII,vector<PII>,greater<PII>>heap;
    heap.push({0,1});//插入距离和节点编号
    while(!heap.empty()){
        PII t=heap.top();
        heap.pop();
        int ver=t.second, distance=t.first;
        if(st[ver])continue;
        st[ver]=1;
        for(int i=h[ver];i!=-1;i=ne[i]){
            int j=e[i];
            if(dist[j]>dist[ver]+w[i])//遍历邻接点
            dist[j]=dist[ver]+w[i];
            heap.push({dist[j],j});
        }
    }
    return (dist[n]==inf?-1:dist[n]);
}
void solve(){
    memset(h,-1,sizeof h);
    memset(dist,inf,sizeof dist);
    int m,a,b,c;
    cin>>n>>m;
    while(m--){
    cin>>a>>b>>c;
    add(a,b,c);
    }
    cout<<Dijkstra()<<endl;
}
signed main(){
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int T=1;
    //cin>>T;
    while(T--)solve();
    return 0;
}

注释版：
#include <cstring>
#include <iostream>
#include <algorithm>
#include <queue>//堆的头文件
using namespace std;
typedef pair<int, int> PII;//堆里存储距离和节点编号//数对/二元组
//优先的是 pair 中的第一个元素（距离）的最小值，堆顶元素始终是队列中first最小的pair。
const int N = 1e6 + 10;
int n, m;//节点数量和边数
int h[N], w[N], e[N], ne[N], idx;//邻接表存储图
int dist[N];//存储距离
bool st[N];//存储状态
void add(int a, int b, int c){
    e[idx] = b, w[idx] = c, ne[idx] = h[a], h[a] = idx ++ ;
}

int dijkstra(){
    memset(dist, 0x3f, sizeof dist);//距离初始化为无穷大
    dist[1] = 0;
    priority_queue<PII, vector<PII>, greater<PII>> heap;//小根堆//greater可以使大根堆变成小根堆
    //<优先队列中存储的元素类型,指定优先队列的内存存储方式<且vector是pair>，比较器的作用类型>
    //greater<PII>父节点与子节点比较，if (greater)true 不调整；else 调整； 父节点要始终大于(新来的)子节点，所以堆顶始终是最小的
    heap.push({0, 1});//插入距离和节点编号
    while (heap.size()){
       /*PII=*/ auto t = heap.top();//取距离源点最近的点
        heap.pop();
        int ver = t.second, distance = t.first;//ver:节点编号，distance:源点距离ver 的距离
        if (st[ver]) continue;//如果距离已经确定，则跳过该点
        st[ver] = true;

        for (int i = h[ver]; i != -1; i = ne[i])//更新ver所指向的节点距离
        {
            int j = e[i];
            if (dist[j] > dist[ver] + w[i]){
                dist[j] = dist[ver] + w[i];
                heap.push({dist[j], j});//距离变小，则入堆
            }
        }
    }
    if (dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}
int main(){
    scanf("%d%d", &n, &m)；
    memset(h, -1, sizeof h);
    while (m -- ){
        int a, b, c;
        scanf("%d%d%d", &a, &b, &c);
        add(a, b, c);//不用去判断重边，因为都储存在里面了
    }
    cout << dijkstra() << endl;
    return 0;
}
```

*使用小根堆后，找到 t 的耗时从 O(n^2) 将为了 O(1)。每次更新 dist 后，需要向堆中插入更新的信息。所以更新dist的时间复杂度有 O(m) 变为了 O(elogn)。总时间复杂度有 O(n^2) 变为了 O(n + mlongn)。适用于稀疏图。*

