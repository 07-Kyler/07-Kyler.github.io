# 题目：[Kadomatsu Subsequence](https://atcoder.jp/contests/abc439/tasks/abc439_d)

**标签：** #模拟 #哈希表 #unodered_map
## 题意描述

给你一个长度为 N 的整数序列 A（下标从 1 到 N）。 求满足以下所有条件的有序三元组 (i, j, k) 的个数：

- $1 ≤ i, j, k ≤ N$ （i, j, k 可以相同或不同）
- $A_i : A_j : A_k = 7 : 5 : 3$（当且仅当$A_i : A_j : A_k = 7t : 5t:3t$ ）
- $min( i , j , k ) = j$  or  $max( i , j , k ) = j$

数据范围：
- 1 ≤ N ≤ 3×10⁵
- 1 ≤ Aᵢ ≤ 10⁹
 
----
## 题面翻译

给定一个数组找出满足条件的组数 数据比较大

---

## 解题思路

第一个条件：只要满足 i j k 都是有效下标以内即可 并不要求需要按照 i j k 的 顺序

二三号条件：看到  *j*  位置比较特殊 如果能确定 j 位置上的数据大小那么就确定了 t 的大小（x\[j] = 5t)
能确定t的大小 再根据二号条件我就能知道x\[i]、x\[k]上的数应该是多少 （每一个t对应了三个固定的数）

三号条件约束了 j 一定是三个下标中最大或最小的 考虑直接遍历 （遍历天然的形成当前下标是最大或最小的状态） 把当前位置看为 j  以当前位置统计<u>前面</u>（对于遍历顺序来讲）已经被遍历过的数 就能保证 j 一定是最大或最小下标（正反顺序两次遍历即可实现最大和最小）

但是N的大小是3e5 每次遍历到一个j再重新遍历一边j前遍历过的数会TLE 想到可以用桶思想把前面每一个数出现的次数先统计好 当找到x\[j]的时候直接调用当前t对应的7t和3t（均为下标）即可 

但是！数组数据几乎要超过int的范围了 这时候再定义一个超级大的桶是不太可能了 

这样的情况就要引入[[unordered_map]]（哈希表：相当于是python里的字典）不需要一个具体的下标 只需要给定的一个值c 用哈希表调用 mp\[c] 就能得到对应的一个值 这里直接把这个值当作计数器使用 

哈希表初始值为 0

在这个题目中 每遍历到一个 j 就计算当前 j 位置的贡献  
	`t = x[j]/5;  ans+=mp[t*7]+mp[t*3];`
注意要先计算贡献再将当前位置统计进哈希表 否则会把当前位置算进贡献中 ( i != j != k ) 

注意要在正反顺序遍历的中间加一句
	`mp.clear();`
防止上一次的数据被统计进下一次

数据大 记得开 long long 

---


${{\Huge Code}}$
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
unordered_map<int,int> mp;
int n,t;
int cnt7 = 0,cnt3 = 0;
vector<int> x;

signed main (){
    cin>>n;
    x.resize(n+10);//
    for(int i = 1;i<=n;++i){
        cin>>x[i];
    }

    int cnt = 0;
    for(int i = 1;i<=n;++i){
        if(x[i]%5 == 0)cnt+=mp[x[i]/5*3]*mp[x[i]/5*7];
        mp[x[i]]++;
    }
    mp.clear();
    for(int i = n;i>=1;--i){
        if(x[i]%5 == 0)cnt+=mp[x[i]/5*3]*mp[x[i]/5*7];
        mp[x[i]]++;
    }

    cout<<cnt<<endl;
    return 0;
}
```