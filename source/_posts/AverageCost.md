---
title: 经典算法的平均复杂度分析
mathjax: true
date: 2019-04-23
categories:
- 算法
tags:
- 平均时间复杂度
- 算法
---
# 改进的冒泡排序
由于没有改变相邻逆序对互换的本质，数组内平均有$n^2$的逆序对就决定了算法必然复杂度为$\Omicron(n^2)$

# Quick Sort
设`排好序的序列为Z[1:N]`,则认定`指标随机变量`如下：
<font size = 4><center>$X_{ij}=I\{Z_{i}与Z_{j}在QS的过程中发生了比较\}$</center><font size=3>
设算法时间复杂度为$T(n)$,则有：
$$ 
\begin{aligned}
T(n) = & E[\sum_{i<j} X_{ij}] \\
= & \sum_{i<j} E[X_{ij}] \\
= & \sum_{i<j} PR\{Z_{i}与Z_{j}比较的概率\}
\end{aligned}
$$
而$Z_{i}与Z_{j}$会不会进行比较需要看算法是如何进行的，在QS中即是看pivot如何选：
1. 若pivot选择$[Z_{1},Z_{i})\bigcup(Z_{j},Z_{n}],则对它们比不比较没有影响$
2. 若pivot选择$Z_{i}和Z_{j}$则它们必会比较
3. 若pivot选择$(Z_{i}和Z_{j})$则它们必不会比较
    
将不影响结果的区间去除，那么$Z_{i}与Z_{j}$进行比较的概率即是$\frac{2}{j-i+1}$
于是结果即是：
$$
\begin{aligned}
\sum_{i<j} \frac{2}{j-i+1}\in \Omicron(nlogn)
\end{aligned}
$$


# 闭哈希查找

## 失败查找
设哈希表大小为m，内有n个元素

因为失败查找一定会将链长全部走完，因此若记$\frac{n}{m}=\alpha$（平均链长）则有：
$$
\begin{aligned}
T(n)\in \Theta(1+\alpha)
\end{aligned}
$$

## 成功查找
设哈希表大小为m，内有n个元素，将表内元素`按入表顺序排序`,排好的序列记为Z[1:n]，算法的时间复杂度为`T(n)`,则有：
$$
\begin{aligned}
T(n)=&\frac1n *\sum_{i=1}^n (1+\sum_{j=i+1}^n\frac1m)\\
=&1+\frac1n*\sum_{i=1}^n\frac{n-i}{m}\\
=&1+\frac{1}{nm}*\sum_{i=1}^n (n-i)\\
\in\;&\Theta (1+\frac{n^2}{nm})\\
\in\;&\Theta (1+\frac{n}{m})
\end{aligned}
$$
若记$\frac{n}{m}=\alpha$则有：
$$
\begin{aligned}
T(n)\in \Theta(1+\alpha)
\end{aligned}
$$

# 开哈希表查找
有点过于复杂...懒得写出来了，大概意思与闭hash差不多，平均查找长度的求解涉及太多了，全是gay论

