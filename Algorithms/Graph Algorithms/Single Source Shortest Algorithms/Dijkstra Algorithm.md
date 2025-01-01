#graph #algorithms #greedy #heaps
## Ref :
- [Find Shortest Paths from Source to all Vertices using Dijkstra’s Algorithm](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)
- [Find Shortest Paths from Source to all Vertices using Dijkstra’s Algorithm](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)
- [Dijkstra’s Algorithm for Adjacency List Representation | Greedy Algo-8 - GeeksforGeeks](https://www.geeksforgeeks.org/dijkstras-algorithm-for-adjacency-list-representation-greedy-algo-8/?ref=header_outind)
## Dijkstra Algorithm
- It works properly when all edge weights are **non-negative**
- ### Relaxation
	- ![](https://i.imgur.com/APjDb76.png)
## Code
```pseudo
DIJKSTRA(G,w,s)
1	INITIALIZE-SINGLE-SOURCE(G,s)
2	S ={}
3	Q = G.V
4	while Q != {}
5		u = EXTRACT-MIN(Q)
6		S = S ∪ {u}
7		for each vertex v ∈ G.Adj[u]
8			RELAX(u,v,w)
9			DECREASE-KEY(G,v,v.key)
```
## Complexity
- using [[Heap]]
	- line 1 ~ 3 : $O(V+E)$
	- line 5 : $V * O(\lg V)$
	- line 9 : $E * O(\lg V)$
- Running time
	- $O(V^2)$ if we use an (unsorted) array (A lot of edges)
	- $O(V\lg V+ E\lg V)$ if we use a heap (Small edges)
	- $O(V\lg V+E)$ if we use a Fibonacci heap (Best optimal)