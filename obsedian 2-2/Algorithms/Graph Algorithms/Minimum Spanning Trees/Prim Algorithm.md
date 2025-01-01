#mst #algorithms #graph #tree #greedy 
## Ref
- [최소 신장 트리(MST)를 위한 Prim 알고리즘 - GeeksforGeeks](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/?ref=gcse_outind)
- [Prim's Algorithm (Simple Implementation for Adjacency Matrix Representation) - GeeksforGeeks](https://www.geeksforgeeks.org/prims-algorithm-simple-implementation-for-adjacency-matrix-representation/?ref=gcse_outind)
## Prim Algorithm
- Greedy Algorithms
	1. Determine an arbitrary vertex as the starting vertex of the MST
	2. Loop
		1. Find edges connecting any tree vertex with the fringe vertices
		2. Find the minimum among these edges (Greedy)
		3. Add the chosen edge to the MST if does not form any cycle
- [Time Complexity](https://www.geeksforgeeks.org/time-and-space-complexity-analysis-of-prims-algorithm/)
	- $O(V^2)$, but if you using adjacency list, min-heap, It can be reduced.
## Code
- Using [[Heap|MIN-HEAP]]
```pseudo
MST-PRIM(G,w,r)
1	for each u ∈ G.V
2		u.key = ∞
3		u.π = NIL
4	r.key = 0
5	Q = G.V
6	while Q != {}
7		u = EXTRACT-MIN(Q)
8		for each v ∈ G.Adj[u]
9			if v ∈ Q and w(u,v) < v.key
10				v.π = u
11				v.key = w(u,v)
12				DECREASE-KEY(G,v,v.key)    // update min-heap
```

## Complexity
- Time complexity : $\Theta(E\lg V))$
	- line 1 ~ 6 : $\Theta(V)$
	- line 7 : $\Theta(\lg V * V)$
	- line 8 ~ 11 : $\Theta(E)$
	- line 12 : $\Theta(\lg V * E)$
