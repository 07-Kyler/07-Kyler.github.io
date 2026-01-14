# 题目：[Way Too Long Words](https://codeforces.com/problemset/problem/71/A)

**标签：** #字符串 #string
## 题意描述

我们把长度 严格超过 10 个字符的单词称作 太长 单词。所有太长的单词都要换成一种特别的缩写形式。

这种缩写的规则是：写下单词的第一个和最后一个字母，中间写上这两个字母之间的字母数量（用十进制数字表示，且不带前导零）。

比如，“localization”会变成“l10n”，“internationalization”会变成“i18n”。

现在请你帮忙自动完成这个替换过程。所有太长的单词都要换成缩写，其他单词保持原样。

----
## 题面翻译

缩写单词使之符合题目要求的格式

---

## 解题思路

唯一一个坑点在于用getline(cin,x)读入的时候第一次循环会将给的n后面的一个换行符\n一起都进去 导致输出的时候会少一行数据 所以要在cin>>n 之后加一句 cin.ignore( )

string 属于STL的一种容器 定义变量的时候不需要给长度 会自己分配内存

---


${{\Huge Code}}$
```cpp
//CodeForces - 71A Way Too Long Words 

#define endl "\n"
#include<bits/stdc++.h>
using namespace std;

int n;
string x;

int main (){
    cin>>n;
    cin.ignore();
    for(int i = 0;i<n;++i){
        getline(cin,x);
        if(x.size()>10){
            int len = x.size();
            cout<<x[0]<<len-2<<x[x.size()-1]<<endl;

        }else{
            cout<<x<<endl;
        }
        
    }
    return 0;
}


```