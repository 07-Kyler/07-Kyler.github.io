# 题目：[求和]([P3106 - 求和 - ZJHUOJ](http://172.20.8.83/problem.php?id=3106))

**标签：** #数据范围
## 题意描述

给定一个数字n，后面给定n个正整数 求这n个数据之和

由于数据可能比较大所以只需要套输出结果对 $2^{64}$ 取模

#### 输入

第一行输入一个正整数 $n (1≤n≤10^6)$，表示序列中元素的个数。  
  
第二行输入 nn 个正整数 $ai (0≤a_i<2^64)$，两个数之间用空格隔开。

----
## 题面翻译

不再赘述

---

## 解题思路

结果取模这句话纯吓人用的 $2^{64}$ 对应的就是 unsigned long long 的范围 $[0,2^{64}-1]$ 结果超过了这个范围会自动溢出（也就是对 $2^{64}$ 取模） 所以只需要开unsigned long long 正常读入加和再输出即可不需要再手动取模一边

数据个数比较多 用cin cout要写加速语句

---


${{\Huge Code}}$
```cpp
#include<bits/stdc++.h>
using namespace std;

unsigned long long ans = 0,n,t;

int main (){
    cin>>n;
    for(int i = 0;i<n;++i){
        cin>>t;
        ans+=t;
    }
    cout<<ans;
}
```