---
title: 图遍历
mathjax: true
date: 2019-06-16
categories: 
- 算法
- 图论
tags:
- 算法
- 图论
- 图遍历
---

# 基本概念
- 边
  - TE：遍历序指定的边
  - BE：指向（非父）祖先节点
  - DE：指向孙子
  - CE：指向兄弟
  - 写伪代码的时候可以直接写`if uv is BE:`

# DFS
- 有向图中$(u,v)$
  - TE：指白
  - BE：指灰
  - DE：$f[v]<d[u]$ 且指向黑
  - CE：$f[v]\ge d[u]$ 且指向黑
- 无向图中$(u,v)$
  - TE: 指白
  - BE：指灰（将原来有可能是DE与CE的边全部变成BE）
- 割点割边算法：
  - 割点的判定：
    - 根节点：至少有两个子树
    - 其他节点:子点$back\ge discover$
  - 割边的判定
    - 子点$back> discover$
  - 注：当为BE时，更新u.back=min(u.back,v.discover),这里不能是v.back，理由是不能通过割（祖先）点到更远的地方
- 判断有无环：有无BE
- 活动区间对边(u,v)的刻画：
  - TE：$active(v)\in active(u),且无active(v)\in active(x)\in active(u)$
  - DE：$active(v)\in active(x)\in active(u)$
  - BE：$active(u)\in active(v)$
  - CE: $active(v) 在active(u)之前$
- 其他应用：
  - 拓扑排序
  - 关键路径：
    - 算法：利用eft与est
    - （排队，选课）
  - SCC转换G为DAG（有向无环图）：
    - 算法：dfs入栈，转置G，栈序dfs
    - 影响力问题
    - 到达所有点问题
  - 底图定向使得入度为1（判断有无环）
  - 判断是否存在包含特定边e(u,v)的环：去掉e之后从u点dfs若到达v则有，否则无

# BFS
- 颜色
  - 注意：在BFS中，在队列里的颜色就是灰色
  - TE树构成最短路

- 有向图中$(u,v)$
  - TE：指白
  - BE：指黑且是祖先
  - CE：指黑/灰且不是祖先
- 无向图中$(u,v)$
  - TE: 指白
  - CE：指灰
- 对CE（u,v）的限制
  - 有向图只限制右边，即$v.dis\le u.dis+1$
  - 无向图限制两边，$y.dis<=v.dis\le u.dis+1$
- 应用：
  - 二分图判定（二染色）
  - k度子图判定：初始化队列里多个根节点（所有不是小于k度的顶点）的bfs。话说多个节点的队列才是bfs的精髓吧orz

# 综合应用
- O（n）时间内不可能查环：
  - 对于算法每次询问(u,v)间是否有边，构造对手策略如下：
    - 若u,v间有边会导致图中成环，则u,v无边
    - 否则u,v有边
    - 若最后算法给出答案"有环"，此时图中无环
    - 若最后算法给出答案"无环"，此时算法不可能询问完所有的边，将算法未询问过的边加入图中，则此时图必有环（$\Omicron (n^2)- \Omicron (n) = \Omicron(n^2),\Omicron(n^2)的边必成环$）
- 在DAG图上是否存在唯一的一条路径能访问到所有点：
  - 等价于拓扑序唯一（感觉不怎么显然啊......）/dfs找remain
- 有向图中判断是否有一个点可以到达G中所有点
  - SSC之后判断入度0的点是否唯一
  - 不唯一，则不存在
  - 否则dfs唯一的入度为0的点，若所有点都被dfs到，则存在，否则，不存在
- 2-SAT问题
  - 将src SCC 设false之后 将end SCC 设TRUE，循环。
