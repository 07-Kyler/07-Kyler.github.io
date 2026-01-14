# 题目：[相反数]([P3115 - 相反数Ⅱ - ZJHUOJ](http://172.20.8.83/problem.php?id=3115))

**标签：** #数据类型
## 题意描述

给定一个数$n$，输出他的相反数。

数据范围：$$-2^{63}\leq n<(2)^{63}$$

----
## 题面翻译

不在赘述

---

## 解题思路

这里的数据范围对应的数据大小是 long long ∈ \[ -2^63 , 2^63 - 1 ] 

坑：当题目给的数据是LLONG_MIN的时候取反会导致恰好超过long long的范围多1
所以一定要特判一下数据最小边界的情况 用字符串的形式去掉符号直接输出

---


${{\Huge Code}}$
```cpp
#include<bits/stdc++.h>
using namespace std;

signed main (){
    long long n;
    cin>>n;
    if(n == LLONG_MIN){
        cout<<"9223372036854775808";
    }else{
        cout<<-n;
    }
}
```