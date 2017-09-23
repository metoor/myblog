---
title: a*寻路算法总结
categories: algorithm
tags:
  - node.js
  - a*
date: 2017-08-03 20:16:15
---

## 概述
最近想做一个[RPG](https://baike.baidu.com/item/%E8%A7%92%E8%89%B2%E6%89%AE%E6%BC%94%E6%B8%B8%E6%88%8F/1730573?fr=aladdin&fromid=24462&fromtitle=rpg "点我了解详情")类型的游戏，对于RPG游戏而言寻路算法是非常必要的。现在将它记在博客以便日后复习。这里只是一个简单的实现，等空下来会用二叉堆（[Binary Heaps](http://blog.csdn.net/zxz414644665/article/details/15337107 "点我了解详情")）来实现。
<!-- more -->
在计算机科学中，A*算法广泛应用于寻路和图的遍历。最早是于1968年，由Peter Hart, Nils Nilsson 和Bertram Raphael3人在斯坦福研究院描述了 该算法。是对Dijkstra算法的一种扩展。是一种高效的搜索算法。

这是个比较常用的算法，游戏中的寻路通常会使用这个算法，在理解这个算法之前，先明白几个概念：

## 搜索区域（The Search Area）

搜索区域可以划分为正方形格子，但不限于此，六边形，矩形，平行四边形都可以。因此他们的中心点通常称为节点(Node)，而不是方格(Squares)。

##路径排序(Path Sorting)

在没有任何障碍的地图上，一个节点可以有4个方向甚至8个方向移动可能。那么如何选择走那个路径呢，判断的依据就是这个公式：
f = g + h;

g是起点到指定格子的移动代价，h是指定格子到达终点的估算成本，f值则是两者之和。

假设横纵走一格的代价为10， 对角线为14，那么起点往左走一格的g值为10。 

## 启发函数（Heuristics function）

h值属于估算成本，不同的估算方法对应不同的结果。选取适合的估算方法需要根据实际场景而定。我们成这种估算函数为启发函数，例如，允许4个方向走，那么可以采用曼哈顿距离（Manhattan distance）， 即横向和竖向走到终点的距离之和。启发函数的作用在于，当你把启发代价设定的比实际代价更大时，那么搜索速度会变得更快，但结果可能不是最优的路径。相反，
启发代价比实际的小，那么搜索变慢，得到一个最优路径。这是速度 与最优解之间的权衡

开放列表(Open List)
开放列表实际上是一个待检测的格子列表，对应的，我们把检测过的格子放入Close List中。

以上是A*的关键点，尤其是启发函数，如果没有启发函数，则A*就退化成了Dijkstra算法，是运行效率重要还是找到最佳路径重要，全靠启发函数来调节，因此也被归为启发式算法。

## A*算法的具体步骤：
1. 把起点加入 open list 。
2. 重复如下过程：
3. 遍历 open list ，查找 F 值最小的节点，把它作为当前要处理的节点。
4. 把这个节点移到 close list 。
5. 对当前方格的 8 个相邻方格的每一个方格？
(1). 如果它是不可抵达的或者它在 close list 中，忽略它。否则，做如下操作。
(2). 如果它不在 open list 中，把它加入 open list ，并且把当前方格设置为它的父亲，记录该方格的 F ， G 和 H 值。
(3). 如果它已经在 open list 中，检查这条路径 ( 即经由当前方格到达它那里 ) 是否更好，用 G 值作参考。更小的 G 值表示这是更好的路径。如果是这样，把它的父亲设置为当前方格，并重新计算它的 G 和 F 值。如果你的 open list 是按 F 值排序的话，改变后你可能需要重新排序。
6. 停止，当你
(1). 把终点加入到了 open list 中，此时路径已经找到了
(2). 查找终点失败，并且 open list 是空的，此时没有路径。
7. 保存路径。从终点开始，每个方格沿着父节点移动直至起点，这就是你的路径。

## 使用最小二叉堆优化算法
1. 当一棵二叉树的每个结点都大于它的两个子结点时，被称为堆有序；
{% asset_img 0.png %}
2. 叉堆有两种：最大堆和最小堆。
最大堆：父结点的键值总是大于或等于任何一个子结点的键值；
最小堆：父结点的键值总是小于或等于任何一个子节点的键值。
二叉堆一般都通过"数组"来实现。数组实现的二叉堆，父节点和子节点的位置存在一定的关系。我们将"二叉堆的第一个元素"放在数组索引0的位置。
假设"第一个元素"在数组中的索引为 0 的话，则父节点和子节点的位置关系如下： 
* 索引为i的左孩子的索引是 (2*i+1); 
* 索引为i的左孩子的索引是 (2*i+2); 
* 索引为i的父结点的索引是 floor((i-1)/2);
当插入一个新的节点的时候怎么保持二叉堆任然有序呢？
{% asset_img 1.png %}
假设要在这个二叉堆里入队一个单元，只要在数组末尾加入这个元素，然后把这个元素往上挪，直到挪不动，经过了这种复杂度为Ο(logn)的操作，二叉堆性质没有变化。
当删除节点的时候又该怎样保持二叉堆任然有序呢？
{% asset_img 2.png %}

## 程序运行截图
{% asset_img demoScreenShoot.png %}
好了，就讲到这里了。程序源码[点我查看](https://github.com/metoor/astar "Metoor's github")