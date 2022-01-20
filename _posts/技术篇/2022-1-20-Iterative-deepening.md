---
layout: post
title: AcWing 170. 加成序列 
categories: 算法题 迭代加深
description: 迭代加深
keywords: dfs&bfs的结合
excerpt_separator: <!--more-->
---



迭代加深其实不是新的算法，它更像一种思想，常规dfs的缺陷在于往往浪费时间在搜索深度很大的无用子树上，而答案往往在其他深度比较浅的节点，所以迭代加深的思路是限制深度，先搜完某一个特定深度之后再加深深度进行搜索

<!--more-->

题目链接：

https://www.acwing.com/problem/content/description/172/

![image-20220120155826601](https://tva1.sinaimg.cn/large/008i3skNly1gyk70wttsmj31g90u0ae0.jpg)

限制深度，每次多增加1层深度，此题有两个显而易见的剪枝：

1.从大的数开始枚举这一层的数值

2.path[i]+path[j]是组合而不是排列，可以用st数组进行判重


代码：

```c++
#include<iostream>
using namespace std;
const int N=110;
int path[N];
int n,depth;
bool dfs(int now,int depth){
    if(now==depth)return path[now-1]==n;
    bool st[N]={0};
    for(int i=now-1;i>=0;i--){
        for(int j=i;j>=0;j--){
            int s=path[i]+path[j];
            if(s>n||s<=path[now-1]||st[s])continue;
            st[s]=1;
            path[now]=s;
            if(dfs(now+1,depth))return 1;
        }
    }
    return 0;
}
int main(){
    path[0]=1;
    while(cin>>n,n){
        int k=1;
        while(!dfs(1,k))k++;
        for(int i=0;i<k;i++)cout<<path[i]<<" ";
        cout<<endl;
    }
}
```





