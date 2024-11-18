---
date:
    created: 2024-10-04
    updated: 2024-11-16
readtime: 20
categories:
    - AI
tags:
    - Algorithm
---
# Dijkstra算法概述及Python简单实现

Dijkstra算法（迪克斯特拉算法）是一种用于在加权图中找到单个源点到所有其他顶点的最短路径的算法。
<!-- more -->

荷兰杰出计算机科学家、软件工程师 [Dr. Edsger W. Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) 创建并发布了Dijkstra算法。

必要条件：Dijkstra 只能用在权重为 **正** 的图中，因为计算过程中需要将边的权重相加来寻找最短路径。

![](../../../PageImage/Pasted%20image%2020241016121042.png)

Dijkstra 算法将会寻找出图中节点 `0` 到所有其他节点的最短路径。

## 算法思路

![](../../../PageImage/Pasted%20image%2020241016122055.png)

1、指定一个节点，例如我们要计算 $A$ 到其他节点的最短路径

2、引入两个集合$（S、U）$，$S$集合包含已求出的最短路径的点（以及相应的最短长度），$U$集合包含未求出最短路径的点（以及A到该点的路径，注意 如上图所示，`A->C`由于没有直接相连初始时为$∞$）

3、初始化两个集合，

- $S$集合初始时，只有当前要计算的节点，`A->A = 0`

- $U$集合初始时为` A->B = 4, A->C = ∞, A->D = 2, A->E = ∞`

>  直接连接的定义长度，其他认为不可达。

核心两步骤：

4、从U集合中找出路径 **最短** 的点，加入$S$集合，例如` A->D = 2`

>  这里就是一个核心的排序流程，选择最近的一个点加入集合。

5、更新$U$集合路径，`if ( ‘D 到 B,C,E 的距离’ + ‘AD 距离’ < ‘A 到 B,C,E 的距离’ ) `则更新$U$

> 如果通过新的路径可以让距离变得更短，就更新集合 $U$ 信息。

6、循环执行 4、5 两步骤，直至遍历结束，得到$A$到其他节点的最短路径

![](../../../PageImage/Pasted%20image%2020241016134806.png)

## 算法实现及测试

![](../../../PageImage/Pasted%20image%2020241016140254.png)

```python linenums="1"
def dijkstra(graph, start_vertex):
    # 初始化距离字典和前驱字典
    distances = {vertex: float('infinity') for vertex in graph}
    distances[start_vertex] = 0
    predecessors = {vertex: None for vertex in graph}
    
    # 未处理的顶点集合
    unvisited = set(graph.keys())
    
    while unvisited:
        # 选择最小距离顶点
        current_vertex = min(unvisited, key=distances.get)
        unvisited.remove(current_vertex)
        
        # 更新邻居距离
        for neighbor, weight in graph[current_vertex].items():
            distance = distances[current_vertex] + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                predecessors[neighbor] = current_vertex
                
    return distances, predecessors

def print_path(predecessors, target):
    path = []
    current_vertex = target
    while current_vertex is not None:
        path.insert(0, current_vertex)
        current_vertex = predecessors[current_vertex]
    return ' -> '.join(path)

# 图的表示，使用字典的字典
graph = {
    'A': {'B': 1, 'C': 2, 'D': 7},
    'B': {'A': 1, 'C': 4, 'D': 5},
    'C': {'A': 2, 'B': 4, 'D': 1},
    'D': {'A': 7, 'B': 5, 'C': 1}
}

distances, predecessors = dijkstra(graph, 'A')
print("节点\t距离\t路径")
for vertex in graph:
    if vertex != 'A':  # 源点到自身的路径没有意义
        path = print_path(predecessors, vertex)
        print(f"{vertex}\t{distances[vertex]}\t{path}")
```

输出：

```
节点	距离	路径
B	1	A -> B
C	2	A -> C
D	3	A -> C -> D
```

## 参考资料

[图最短路径算法之迪杰斯特拉算法](https://houbb.github.io/2020/01/23/data-struct-learn-03-graph-dijkstra#%E7%AE%97%E6%B3%95%E5%9B%BE%E8%A7%A3)


