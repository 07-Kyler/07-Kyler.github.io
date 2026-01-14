# 题目：[洛谷P2855 [USACO06DEC] River Hopscotch S](https://www.luogu.com.cn/problem/P2855)

**标签：** #二分答案  

## 题目描述

奶牛们每年都会举办一次活动，内容是一种奇特的跳房子游戏，即在河中小心翼翼地从一块石头跳到另一块石头。 比赛在一条笔直的长河上进行，起点有一块石头，终点有另一块石头，距离起点 $L$ 个单位（$1 \le L\le 1,000,000,000$）。 在起点和终点岩石之间的河道上，会出现 $N$ 个（$0\le N\le 50,000 $ 个）更多的岩石，每个岩石与起点的距离为一个整数 $D_i$（$0<D_i<L$）。

玩游戏时，每头牛依次从起点岩石开始，努力到达终点岩石，只能从一个岩石跳到另一个岩石。 当然，不那么灵活的奶牛永远也到不了终点岩石，最后只能掉进河里。

农场主约翰为自己的奶牛感到骄傲，每年都会观看这项比赛。 但随着时间的推移，他已经厌倦了看着其他农户的胆小的奶牛一瘸一拐地走过石头之间的短距离。 他计划移走几块石头，以增加奶牛跳到终点的最短距离。 他知道自己无法移走起点和终点的石头，但他计算出自己有足够的资源移走最多 $M$ 块石头（$0 \le M \le N$）。

FJ 想知道，在开始移走石头之前，他能将最短距离增加多少。 请帮助农场主约翰确定在移走最优的 $M$ 组石块后，奶牛要跳过的最短距离。

形式化中文题意：

对于给定在一维位置的 $N$ 个点，选择 $M$ 个点进行移除，使得每两个点之间的距离最小值最大。

**输入格式**：

第 $1$ 行，三个空格分隔的整数：$L$、$N$ 和 $M$。


第 $2\dots N+1$ 行，每行包含一个整数，表示某块岩石距离起始岩石的距离。 没有两块石头的位置相同。



----
## 题面翻译

总共有n个位置上有石头 其中移走m块石头 使移走之后所有石头的间距的最小值最大 

---

## 解题思路

最小值最大 二分的特征 二分可能的最小值 带入石头的距离中贪心 如果当前这个石头跟上一个石头的间距够大就不移动 否则就跳过当前石头（充当移动的操作 实际上数组是没有变的）移动次数++ 最后与移动次数M相比  

这里给定的数据是 “某一个石头距离原点的距离” 并没有说是按照石头的先后顺序给定的 所以要先按照距离大小排序才能二分

---


${{\Huge Code}}$
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
int l,n,m;
vector<int> x;
vector<int> gap;//gap[i]表示第i个石头到i-1个石头的距离
bool check(int gp);
int mn = 1e9;


signed main (){
    cin>>l>>n>>m;
    x.resize(n+2);
    x[0] = 0;
    x[n+1] = l;
    gap.resize(n+2);
    for(int i = 1;i<=n;++i){
        cin>>x[i];
        // gap[i] = x[i]-x[i-1];
        // mn = min(mn,gap[i]);
    }
    //gap[n+1] = x[n+1]-x[n];
    sort(x.begin(),x.end());
    int left = 1,right = l;
    while(left<right){
        int mid = (left+right+1)/2;
        if(check(mid)) left = mid;
        else right = mid-1;
    }
    cout<<left<<endl;
    return 0;
}
bool check(int gp){
    // if(mn>=gp){
    //     return true;
    // }
    int remove = 0;
    int last = 0;
    for(int i = 1;i<=n+1;++i){
        if(x[i]-last<gp){
            remove++;
        }else{
            last = x[i];
        }
    }
    return remove<=m;
    
}
```