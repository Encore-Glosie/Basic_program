# [338. 计数问题 - AcWing题库](https://www.acwing.com/problem/content/340/)
```cpp
#include<stdio.h>
#include<iostream>

#define ll long long

using namespace std;

int power10(int x)//返回10的x次方
{
    int res=1;
    while(x--)res*=10;
    return res;
}

ll count(int n,int x)//返回从1~n所有数中x的总数
{
    ll res=0;
    int l,r,cnt=0,m=n;

    while(m)
    {
        cnt++;//存储数字n的位数
        m/=10;
    }

    for(int i=1;i<=cnt;i++)//从右往左依次枚举每一位上的x总数
    {
        //以abcdefg为例来看，现在是计算第四位上x的次数，那么现在i=4

        //先计算最高三位为000~abc-1的情况
        r=power10(i-1);//d右边可取到000~999共power10(i-1)个数
        l=n/(r*10);//d左边可取到000~abc-1共abc种情况，if(x==0)则为001~abc-1共abc-1种
        //abc=n/power10(i)=n/(r*10);
        if(x)res+=l*r;
        else res+=(l-1)*r;

        int d=(n/r)%10;// n/r=abcd;abcd%10=d;
        
        //再计算高三位等于abc的情况(只需考虑d>=x，因为d<x就不符合条件)
        if(d==x)//前四位abcd均相同，后三位可取0~efg共efg+1种
            res+=n%r+1;//efg+1=n%power(i-1)+1=n%r+1;
        else if(d>x)//此时后三位可取000~999共power10(i-1)种
            res+=r;
    }
    return res;
}
int main()
{
    int a,b;
    while(cin>>a>>b,a||b)
    {
        if(a>b)swap(a,b);

        for(int i=0;i<10;i++)
            cout<<count(b,i)-count(a-1,i)<<" ";

        cout<<"\n";
    }
    return 0;
}


```