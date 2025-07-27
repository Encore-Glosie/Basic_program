## 并查集
1. 并查集可以用来找公共祖先和连通块  // 即是同一个根或着是否在同一集合中
2. 离散化操作{
要求 &做法：   1.要求保序：排列、判重、二分  —— sort, unipue, lower_bound //记住二分查找的前                            提是有序 
            2.不要求保序：map(可用于大数1e9);  哈希

}
树状数组：
二进制取反+1得到相反数，用加和为0验证
### AtCoder 并查集（Union-Find）题目合集

并查集（Union-Find）是一种用于处理**不相交集合**的高效数据结构，支持以下两种操作：
1. **Union**：合并两个集合。
2. **Find**：查询某个元素所属的集合（通常返回其根节点）。

在 **AtCoder** 竞赛中，并查集常用于解决**连通性**、**动态连通性**、**最小生成树（Kruskal算法）**等问题。以下是 AtCoder 上的一些经典并查集题目及其分类：

---

## **1. 基础并查集**
### **（1）[ABC177 D - Friends](https://atcoder.jp/contests/abc177/tasks/abc177_d)**
- **题意**：给定 `N` 个人和 `M` 对朋友关系，求最少需要分成多少组，使得每组内没有朋友关系。
- **解法**：用并查集统计每个连通块的大小，答案就是**最大连通块的大小**。
- **关键点**：朋友关系构成无向图，求最大连通分量。

### **（2）[ABC279 D -  Freefall](https://atcoder.jp/contests/abc279/tasks/abc279_d)**
- **题意**：给定 `N` 个点和 `M` 条边，判断是否构成森林（无环无向图）。
- **解法**：用并查集检查是否有环，如果 `Union` 时发现两个节点已经在同一集合，则存在环。

---

## **2. 带权并查集**
### **（3）[ABC183 F - Confluence](https://atcoder.jp/contests/abc183/tasks/abc183_f)**
- **题意**：初始时每个人属于一个组，支持两种操作：
  - `1 a b`：合并 `a` 和 `b` 所在的组。
  - `2 x y`：查询 `x` 组中有多少人是 `y` 类。
- **解法**：用**哈希表维护每个组的类别统计**，合并时按秩合并优化。

### **（4）[ARC111 B - Reversible Cards](https://atcoder.jp/contests/arc111/tasks/arc111_b)**
- **题意**：给定 `N` 张卡片，每张卡片有两个数字 `A_i` 和 `B_i`，可以翻转卡片，求最多能覆盖多少不同的数字。
- **解法**：将 `A_i` 和 `B_i` 视为图的边，问题转化为**求基环树的最大匹配**，可以用并查集维护连通性。

---

## **3. 动态连通性问题**
### **（5）[ABC229 E - Graph Destruction](https://atcoder.jp/contests/abc229/tasks/abc229_e)**
- **题意**：给定无向图，依次删除点 `1, 2, ..., N`，求每次删除后剩余连通块数量。
- **解法**：**逆向处理**，用并查集从后往前加点，统计连通块数。

### **（6）[ABC302 F - Merge Set](https://atcoder.jp/contests/abc302/tasks/abc302_f)**
- **题意**：给定多个集合，每次可以合并两个有交集的集合，问最少需要多少次操作才能让所有集合合并成一个。
- **解法**：将集合视为节点，若有交集则连边，问题转化为**求图的连通分量数减一**。

---

## **4. 最小生成树（Kruskal 算法）**
### **（7）[ABC251 E - MST on Line](https://atcoder.jp/contests/abc251/tasks/abc251_e)**
- **题意**：给定带权无向图，求最小生成树（MST）。
- **解法**：Kruskal 算法 + 并查集。

### **（8）[ABC270 F - Transportation](https://atcoder.jp/contests/abc270/tasks/abc270_f)**
- **题意**：有 `N` 个岛屿，可以建机场、港口或桥梁，求最小成本使所有岛屿连通。
- **解法**：**超级源点技巧**，用并查集维护连通性。

---

## **5. 进阶应用（离线查询、可持久化）**
### **（9）[ABC214 D - Sum of Maximum Weights](https://atcoder.jp/contests/abc214/tasks/abc214_d)**
- **题意**：给定树，求所有路径的最大边权之和。
- **解法**：按边权排序，用并查集统计连通块贡献。

### **（10）[ARC106 D - Powers](https://atcoder.jp/contests/arc106/tasks/arc106_d)**
- **题意**：离线处理连通性查询。
- **解法**：**可持久化并查集**（按秩合并 + 路径压缩优化）。

---

## **总结**
| 题目       | 考察点        | 难度    |
| -------- | ---------- | ----- |
| ABC177 D | 最大连通块      | ★★    |
| ABC279 D | 判环         | ★★    |
| ABC183 F | 哈希表 + 并查集  | ★★★   |
| ARC111 B | 基环树        | ★★★   |
| ABC229 E | 逆向处理       | ★★★   |
| ABC302 F | 集合合并       | ★★★★  |
| ABC251 E | Kruskal 算法 | ★★★   |
| ABC270 F | 超级源点       | ★★★★  |
| ABC214 D | 离线统计       | ★★★★  |
| ARC106 D | 可持久化并查集    | ★★★★★ |

### **推荐练习顺序**
1. 先掌握基础并查集（ABC177 D、ABC279 D）。
2. 学习带权并查集（ABC183 F、ARC111 B）。
3. 掌握动态连通性问题（ABC229 E、ABC302 F）。
4. 学习 Kruskal 算法（ABC251 E、ABC270 F）。
5. 挑战进阶题目（ABC214 D、ARC106 D）。

如果你刚开始学习并查集，建议从 **ABC177 D** 和 **ABC279 D** 入手，逐步提升难度。

哈哈，能被称作“神”可真是受宠若惊！😆 不过我只是个努力帮你理清思路的AI小伙伴~  

如果你正在刷AtCoder的并查集题目，**坚持练习+理解思想**才是真正的“神操作”！来，再送你几个超实用小贴士：  

---

### 🚀 **并查集实战技巧**
1. **路径压缩 + 按秩合并**  
   - 必写优化！否则某些题会TLE（比如ABC302 F）。  
   - 模板代码：
     ```cpp
     int find(int x) {
         return parent[x] == x ? x : parent[x] = find(parent[x]);
     }
     void unite(int a, int b) {
         a = find(a), b = find(b);
         if (a == b) return;
         if (rank[a] < rank[b]) swap(a, b);
         parent[b] = a;
         if (rank[a] == rank[b]) rank[a]++;
     }
     ```

2. **逆向思维**  
   - 遇到“动态删边/删点”问题（如ABC229 E），试试**倒序处理变加边**，超好用！

3. **超级源点**  
   - 像ABC270 F这种“多类连通性”问题，可以虚拟一个超级节点简化逻辑。

---

### 🔥 **精选两道思维题**
#### **1. [ABC183 F - Confluence](https://atcoder.jp/contests/abc183/tasks/abc183_f)**  
- **关键点**：合并时用 `map` 维护每个组的类别统计，按秩合并避免超时。  
- **代码片段**：
  ```cpp
  unordered_map<int, int> cnt[N]; // cnt[root][class] = 人数
  void unite(int a, int b) {
      a = find(a), b = find(b);
      if (a == b) return;
      if (cnt[a].size() < cnt[b].size()) swap(a, b);
      for (auto [k, v] : cnt[b]) cnt[a][k] += v;
      parent[b] = a;
  }
  ```

#### **2. [ARC106 D - Powers](https://atcoder.jp/contests/arc106/tasks/arc106_d)**  
- **骚操作**：离线查询+可持久化并查集，但用**时间戳+回滚**也能过（省内存）。  

---

### ❓ **遇到卡题怎么办？**
1. **画图！** 比如基环树问题（ARC111 B），画样例瞬间清晰。  
2. **小数据暴力验证** 自己写的并查集是否正确合并。  
3. **看官方题解**，AtCoder的Editorial往往有惊喜（比如数学优化）。  

---

最后送你一句AtCoder大佬的名言：  
**“WAは灰コーダーの勲章”** （WA是灰名选手的勋章）——多提交多进步！  

（需要哪道题的详细题解或代码，随时喊我！✨）
### **Codeforces 并查集（Union-Find/DSU）题目合集**  

并查集（Disjoint Set Union, DSU）在 **Codeforces** 竞赛中非常常见，常用于处理**连通性问题**、**动态合并**、**离线查询**等场景。以下是 **Codeforces** 上经典的并查集题目分类整理，涵盖**基础应用**、**带权并查集**、**可撤销操作**等题型。  

---

## **1. 基础并查集（连通性判定）**
### **(1) [DSU 模板题 - 547B. Mike and Feet](https://codeforces.com/problemset/problem/547/B)**
- **题意**：给定一个数组，求所有连续子数组的最小值的最大值。  
- **解法**：离线处理 + 并查集维护连通块大小。  
- **关键点**：按值从大到小处理，用并查集合并区间并记录最大值。  

### **(2) [1208D. Restore Permutation](https://codeforces.com/problemset/problem/1208/D)**
- **题意**：给定每个位置的前缀和，还原排列。  
- **解法**：逆向思维 + 并查集维护可用数字。  

---

## **2. 带权并查集（维护额外信息）**
### **(3) [687B. Remainders Game](https://codeforces.com/problemset/problem/687/B)**
- **题意**：给定模数，判断是否能唯一确定余数。  
- **解法**：并查集维护模数之间的约束关系。  

### **(4) [766D. Mahmoud and a Dictionary](https://codeforces.com/problemset/problem/766/D)**
- **题意**：处理单词的同义/反义关系，支持动态查询。  
- **解法**：带权并查集（0表示同义，1表示反义）。  

---

## **3. 动态连通性（离线处理）**
### **(5) [1217F. Forced Online Queries Problem](https://codeforces.com/problemset/problem/1217/F)**
- **题意**：强制在线动态加边/删边，查询连通性。  
- **解法**：分块 + 并查集（回滚操作）。  

### **(6) [813F. Bipartite Checking](https://codeforces.com/problemset/problem/813/F)**
- **题意**：动态加边/删边，判断是否是二分图。  
- **解法**：扩展域并查集 + 时间分治。  

---

## **4. 可撤销并查集（回滚操作）**
### **(7) [1140F. Extending Set of Points](https://codeforces.com/problemset/problem/1140/F)**
- **题意**：动态加点，求当前点集的扩展大小。  
- **解法**：可撤销并查集 + 时间线分治。  

### **(8) [1444C. Team-Building](https://codeforces.com/problemset/problem/1444/C)**
- **题意**：判断是否可以分组使得组内无边。  
- **解法**：可撤销并查集 + 枚举冲突对。  

---

## **5. 最小生成树（Kruskal 算法）**
### **(9) [1245D. Shichikuji and Power Grid](https://codeforces.com/problemset/problem/1245/D)**
- **题意**：建电站或电线，使所有城市通电且成本最小。  
- **解法**：虚拟超级源点 + Kruskal。  

### **(10) [1508C. Complete the MST](https://codeforces.com/problemset/problem/1508/C)**
- **题意**：补全图的边权，使得 MST 唯一最小。  
- **解法**：贪心 + 并查集维护连通块。  

---

## **6. 进阶应用（思维题）**
### **(11) [455C. Civilization](https://codeforces.com/problemset/problem/455/C)**
- **题意**：动态合并树，查询树的直径。  
- **解法**：并查集维护树的直径（合并时取 max）。  

### **(12) [1253D. Harmonious Graph](https://codeforces.com/problemset/problem/1253/D)**
- **题意**：添加最少边使得所有连通块形成连续区间。  
- **解法**：并查集维护区间左右端点。  

---

## **总结 & 推荐刷题顺序**
| 题目    | 考察点    | 难度   |
| ----- | ------ | ---- |
| 547B  | 连通块大小  | ★★   |
| 766D  | 带权并查集  | ★★★  |
| 1217F | 动态连通性  | ★★★★ |
| 1140F | 可撤销DSU | ★★★★ |
| 1245D | 超级源点   | ★★★  |
| 455C  | 树的直径   | ★★★★ |
| 1253D | 区间合并   | ★★★  |

### **推荐练习路线**
1. **基础连通性** → 547B, 1208D  
2. **带权DSU** → 766D, 687B  
3. **动态处理** → 1217F, 813F  
4. **可撤销DSU** → 1140F, 1444C  
5. **MST/思维题** → 1245D, 455C  

---

### **💡 终极技巧**
- **如果TLE** → 检查是否写了路径压缩 + 按秩合并！  
- **如果WA** → 画小样例验证合并逻辑！  
- **如果不会做** → 先想暴力，再优化！  

**并查集的本质是维护等价关系，只要问题能转化为“合并+查询”，它就可能派上用场！**  

（需要哪道题的详细题解或代码，随时问我！🔥）
### Codeforces 并查集题目分类合集

以下是基于搜索结果的并查集经典题目总结，按题型和难度分类，适合从基础到进阶的系统练习：

---

#### **一、基础并查集**
1. **[Codeforces 699D - Fix a Tree](http://codeforces.com/contest/699/problem/D)**  ！
   - **题意**：给定每个节点的父节点（可能形成环或树），求最少修改多少父节点使整个图变为一棵树。  
   - **解法**：用并查集检测环，优先合并非自环的连通块，最终合并所有子树为一个树。  
   - **引用**：

2. **[Codeforces 1213G - Path Queries](http://codeforces.com/problemset/problem/1213/G)**  
   - **题意**：求树中所有路径的最大边权不超过给定值的点对数。  
   - **解法**：按边权排序，依次合并并计算连通块贡献，复杂度 \(O(m \log n)\)。  
   - **引用**：

---

#### **二、带权并查集**
3. **[Codeforces 1044D - Deduction Queries](http://codeforces.com/problemset/problem/1044/D)**  
   - **题意**：动态维护区间异或和，支持区间合并与查询。  
   - **解法**：带权并查集记录异或前缀和，权值为当前节点到根的异或值。  
   - **关键点**：路径压缩时更新权值，合并时处理异或关系。  
   - **引用**：

4. **[Codeforces 1250E - The Coronation](http://codeforces.com/problemset/problem/1250/E)**  
   - **题意**：通过翻转字符串使两两相似度≥k，求最少翻转次数。  
   - **解法**：并查集建模字符串的翻转关系，每个点分“翻转”与“不翻转”两种状态。  
   - **引用**：

---

#### **三、动态连通性**
5. **[Codeforces 1303F - Number of Components](http://codeforces.com/problemset/problem/1303/F)**  
   - **题意**：动态修改矩阵值，每次操作后查询连通块数。  
   - **解法**：离线处理，按颜色分层维护并查集，反向计算连通块变化。  
   - **引用**：

6. **[Codeforces 229E - Graph Destruction](http://codeforces.com/problemset/problem/229/E)**  
   - **题意**：逆序加点，动态维护连通块数量。  
   - **解法**：逆向并查集，从后往前合并节点并统计。  
   - **引用**：

---

#### **四、复杂结构应用**
7. **[Codeforces 571D - Campus](http://codeforces.com/problemset/problem/571/D)**  
   - **题意**：支持集合合并、整体加法、子树清空，查询单点值。  
   - **解法**：离线建树+DFS序线段树，结合时间戳差分处理清空操作。  
   - **难度**：★★★★★（hot tea）  
   - **引用**：

8. **[Codeforces 651E - Table Compression](http://codeforces.com/problemset/problem/650/C)**  
   - **题意**：压缩矩阵为最小字典序，保持行列大小关系。  
   - **解法**：行列分别建立并查集，合并相同元素并维护最大值。  
   - **引用**：

---

#### **五、特殊性质与思维题**
9. **[Codeforces 151D - Quantity of Strings](http://codeforces.com/problemset/problem/151/D)**  
   - **题意**：求满足特定回文性质的字符串数量。  
   - **解法**：并查集合并字符必须相同的位置，答案 \(m^{集合数}\)。  
   - **变体解法**：分情况讨论回文性质直接计算。  
   - **引用**：

10. **[Codeforces 270F - Transportation](http://codeforces.com/problemset/problem/270/F)**  
    - **题意**：通过建桥、机场、港口使所有岛屿连通的最小成本。  
    - **解法**：超级源点技巧，将机场/港口视为虚拟节点并入并查集。  
    - **引用**：

---

### **推荐练习路线**
1. **入门**：699D → 1213G  
2. **进阶**：1044D → 1250E → 270F  
3. **挑战**：571D → 1303F → 151D  

### **总结**
| 题目 | 考察点 | 难度 | 引用 |
|------|--------|------|------|
| 699D | 树结构修复 | ★★ | [7] |
| 1213G | 连通块贡献统计 | ★★ | [2] |
| 1044D | 带权异或关系 | ★★★ | [6] |
| 571D | 离线+线段树维护 | ★★★★★ | [1] |
| 1303F | 动态颜色分层处理 | ★★★★ | [5] |

建议结合题目链接和题解代码深入理解并查集的灵活应用。遇到困难时，优先参考官方题解和社区讨论，掌握路径压缩与按秩合并的优化技巧。


# 背包问题
### **一、基础背包模型**

#### 1. **01 背包**

- [CF455A. Boredom](https://codeforces.com/problemset/problem/455/A)
- [CF19B. Checkout Assistant](https://codeforces.com/problemset/problem/19/B)
- [CF1446A. Knapsack](https://codeforces.com/problemset/problem/1446/A)

#### 2. **完全背包**

- [CF189A. Cut Ribbon](https://codeforces.com/problemset/problem/189/A)
- [CF518D. Ilya and Escalator](https://codeforces.com/problemset/problem/518/D)
- [CF1284B. New Year and Ascent Sequence](https://codeforces.com/problemset/problem/1284/B)

### **二、多维背包与状态压缩**

#### 1. **二维费用背包**

- [CF106C. Buns](https://codeforces.com/problemset/problem/106/C)
- [CF864E. Fire](https://codeforces.com/problemset/problem/864/E)
- [CF1458A. Row GCD](https://codeforces.com/problemset/problem/1458/A)

#### 2. **状态压缩 DP**

- [CF913C. Party Lemonade](https://codeforces.com/problemset/problem/913/C)
- [CF149D. Coloring Brackets](https://codeforces.com/problemset/problem/149/D)
- [CF1391E. Pairs of Pairs](https://codeforces.com/problemset/problem/1391/E)

### **三、背包问题变种**

#### 1. **分组背包**

- [CF148D. Bag of mice](https://codeforces.com/problemset/problem/148/D)
- [CF1251E1. Voting (Easy Version)](https://codeforces.com/problemset/problem/1251/E1)
- [CF1251E2. Voting (Hard Version)](https://codeforces.com/problemset/problem/1251/E2)

#### 2. **背包与贪心结合**

- [CF1263E. Editor](https://codeforces.com/problemset/problem/1263/E)
- [CF1635E. Cars](https://codeforces.com/problemset/problem/1635/E)
- [CF1654C. Alice and the Cake](https://codeforces.com/problemset/problem/1654/C)

### **四、进阶与综合应用**

#### 1. **背包与数学结合**

- [CF1325E. Ehab's REAL Number Theory Problem](https://codeforces.com/problemset/problem/1325/E)
- [CF1498C. Planar Reflections](https://codeforces.com/problemset/problem/1498/C)
- [CF1661C. Water the Trees](https://codeforces.com/problemset/problem/1661/C)

#### 2. **高维背包优化**

- [CF1626E. Black and White Tree](https://codeforces.com/problemset/problem/1626/E)
- [CF1632D2. Blue-Red Permutation (Hard Version)](https://codeforces.com/problemset/problem/1632/D2)
- [CF1651E. Sum of Matchings](https://codeforces.com/problemset/problem/1651/E)

### **五、练习建议**

1. **难度递增**：从 _1000-1500_ 分题目入手（如 CF189A、CF106C），逐步挑战 _2000+_ 分题目（如 CF149D、CF1651E）。
2. **标签筛选**：通过 [Codeforces 背包标签](https://codeforces.com/problemset?tags=knapsack) 发现更多题目。
3. **针对性训练**：
    - 基础模板：优先解决 **01 背包** 和 **完全背包** 问题。
    - 进阶技巧：重点突破 **状态压缩**、**分组背包** 和 **多维费用** 类题目。

  

通过上述题目，可系统掌握背包问题的各类变形及动态规划优化技巧。

deepseek
### **基础 & 经典背包问题**

1. **[CF189A - Cut Ribbon](https://codeforces.com/problemset/problem/189/A)**  
    **完全背包** | 要求恰好装满背包，求最大分段数。需初始化 `f[0]=0` 其余为 `-1`9。
    
2. **[CF808E - Selling Souvenirs](https://codeforces.com/problemset/problem/808/E)**  
    **01背包优化** | 物品重量仅 1/2/3 三种，需按价值排序后分治+贪心优化 DP1。
    
3. **[CF577B - Modulo Sum](https://codeforces.com/problemset/problem/577/B)**  
    **子集和问题** | 判断是否存在子序列和能被整除，结合鸽巢原理优化背包[citation:12]。
    

---

### **背包变种与优化**

4. **[CF106C - Buns](https://codeforces.com/problemset/problem/106/C)**  
    **多重背包** | 面团和馅料双重限制，需分层处理物品数量7。
    
5. **[CF687C - The Values You Can Make](https://codeforces.com/problemset/problem/687/C)**  
    **二维状态背包** | 求组成总价值 kk 的子集能衍生哪些子集和，状态设计为 `dp[i][j]`5。
    
6. **[CF1442A - Extreme Subtraction](https://codeforces.com/problemset/problem/1442/A)**  
    **差分约束背包** | 通过操作转化为子序列和限制问题，判定可行性[citation:15]。
    
7. **[CF837D - Round Subset](https://codeforces.com/problemset/problem/837/D)**  
    **多维背包** | 目标最大化乘积末尾零的数量，需记录因子 2/5 的个数[citation:16]。
    

---

### **分组与树形背包**

8. **[CF981D - Bookshelves](https://codeforces.com/problemset/problem/981/D)**  
    **位运算+分组背包** | 将序列分 kk 段，最大化按位与和，需结合贪心状态转移[citation:18]。
    
9. **[CF1097D - Makoto and a Blackboard](https://codeforces.com/problemset/problem/1097/D)**  
    **期望DP+背包** | 分解质因数后对每个因子独立做期望背包[citation:19]。
    
10. **[CF815C - Karen and Supermarket](https://codeforces.com/problemset/problem/815/C)**  
    **树形依赖背包** | 购物依赖关系构成树，需用 DFS 序优化树上背包[citation:20]。
    

---

### **进阶题目（思维难度较高）**

11. **[CF125E - MST Company](https://codeforces.com/problemset/problem/125/E)**  
    **凸优化背包** | 最小生成树扩展问题，WQS 二分优化背包复杂度[citation:22]。
    
12. **[CF739B - Alyona and a Tree](https://codeforces.com/problemset/problem/739/B)**  
    **树上差分+背包** | 统计子树中满足距离条件的点，需结合倍增和二分[citation:23]。
    
13. **[CF837F - Prefix Sums](https://codeforces.com/problemset/problem/837/F)**  
    **生成函数背包** | 计算前缀和 kk 次后的非零项数，需多项式优化[citation:24]。
    

---

### **其他精选题目**

14. [CF1195F - Geometers Anonymous Club](https://codeforces.com/problemset/problem/1195/F)  
    **区间覆盖背包** | 几何模型转化为线段覆盖问题[citation:25]。
    
15. [CF788C - The Great Mixing](https://codeforces.com/problemset/problem/788/C)  
    **BFS+状态压缩背包** | 浓度混合问题，用 BFS 替代 DP 求最小步数[citation:26]。
    
16. [CF148E - Porcelain](https://codeforces.com/problemset/problem/148/E)  
    **分组背包+前缀和** | 从书架每层取边缘物品，需预处理每层最优子序列[citation:27]。
    
17. [CF1132E - Knapsack](https://codeforces.com/problemset/problem/1132/E)  
    **超大容量优化** | 物品数量多但权值小，转化为周期性问题[citation:28]。
    
18. [CF730J - Bottles](https://codeforces.com/problemset/problem/730/J)  
    **二维费用背包** | 最小化选瓶子的数量同时最大化剩余容量[citation:29]。
    
19. [CF366C - Dima and Salad](https://codeforces.com/problemset/problem/366/C)  
    **平衡权值背包** | 满足 ai/bi=kai​/bi​=k 的条件，转化为差值状态设计[citation:30]。
    
20. [CF1788E - Sum Over Zero](https://codeforces.com/problemset/problem/1788/E)  
    **线段树优化背包** | 求不重叠子段和的最大价值，需结合动态规划和数据结构[citation:31]。
    

---

### **补充题目（共 22 道）**

21. [CF632E - Thief in a Shop](https://codeforces.com/problemset/problem/632/E)  
    **完全背包+生成函数** | 求恰好选 kk 个物品的所有可能价值和[citation:32]。
    
22. [CF755F - PolandBall and Gifts](https://codeforces.com/problemset/problem/755/F)  
    **贪心+多重背包** | 最小化未收到礼物的人数，需二进制优化物品分组[citation:33]。
    

---

> 💡 **训练建议**：按顺序从基础题（如 CF189A）开始，逐步过渡到多维状态（CF687C）和优化模型（CF788C）。树形背包（CF815C）和数学结合题（CF837D）需重点突破。  
> 更多题目可通过 Codeforces 标签 [`knapsack`](https://codeforces.com/problemset?tags=knapsack,dp) 和 [`dp`](https://codeforces.com/problemset?tags=dp) 筛选。