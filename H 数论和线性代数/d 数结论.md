1. [Problem - A - Codeforces](https://codeforces.com/contest/2092/problem/A)
- 因为距离和的最小值通常出现在中位数位置（数学性质）。
- distance(x)=∑​∣x−xi​∣,当x位于所有xi中位数时，distance最小
```cpp
pow((double)a, 2./3.)可以计算 a 的 2/3 方根（ 2.和 3.是为了让其成浮点数，你面阶段成整数）
== cbrt(pow((double)a, 2))
```