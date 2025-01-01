#graph #algorithms #mst #disjoint_set #greedy 

## Reference
- [크루스칼의 최소 스패닝 트리(MST) 알고리즘 - GeeksforGeeks](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/?ref=gcse_outind)
- [크루스칼 알고리즘(인접 행렬에 대한 간단한 구현) - GeeksforGeeks](https://www.geeksforgeeks.org/kruskals-algorithm-simple-implementation-for-adjacency-matrix/?ref=gcse_outind)
## Kruskal Algorithms
- Greedy Algorithm
	1. select minmum weight edge (greedy)
	2. no cycle in spanning tree, add it.
- [[Union-Find Algorithms]] ([[Disjoint Sets]])
## Code
```pseudo
MST-KRUSKAL(G,w)
1	A = {}
2	for each vertex v ∈ G.V
3		MAKE-SET(v)
4	sort the edges of G.E into nondecreasing order by weight w
5	for each edge (u,v) ∈ G.E, taken in nondecreasing order by weight
6		if FIND-SET(u) != FIND-SET(v)
7			A = A ∪ {(u,v)}
8			UNION(u,v)
9	return A
```
## Complexity
- Time complexity : $O(E\lg E)$ It can also represent, $E\leq V^2\rightarrow O(E\lg V)$
	- line 2 ~ 3 : V 
	- line 4 : $O(E\lg E)$
	- line 5 ~ 8 : $O((V+E)\alpha(V))$
		- m : n(V, ref line 3) + f(E, ref line 5) + u(V-1, ref union algorithms)
		- UNION : $O(m\alpha(n)) = O((V+E)\alpha(V))$