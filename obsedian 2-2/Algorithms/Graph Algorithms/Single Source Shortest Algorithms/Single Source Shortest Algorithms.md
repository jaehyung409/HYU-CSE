## Ref : 
- [문제가 있는 최단 경로 알고리즘 튜토리얼 - GeeksforGeeks](https://www.geeksforgeeks.org/shortest-path-algorithms-a-complete-guide/)
## Shortest-Path Problems
- ### Definition
	- Edge weight
	- Path weight
		- The sum of all edge weights in the path
	- ***A Shortest path*** from $u$ to $v$
		- A path from $u$ to $v$ whose weight is the smallest
		- Vertex $u$ is the **source** and $v$ is the **destination**
	- ***The Shortest-path weight*** from $u$ to $v$
		- The weight of a shortest-path from $u$ to $v$
		- $\delta(u,v)$
- ### Problems
	- Single-Source & Single-Destination
	- *** Single-Source (& All-Destination)***
		- An algorithm for singe-source problem can be used to solve all the other problems
	- Single-Destination (& All-Source)
	- All Pairs
- ### Negative-weight edge
	- Single-source shortes paths can be defined if there are noy any ***negative-weight cycles reachable from the source***
		- Cycles
			- There is a shortest path that does not include cycles
			- A shortest-path length is at most $|V| - 1$
- ### Predecessor subgraph
	- Shortest-path tree (stores all SSSPs compactly)
	- Optimal substructure
## In Directed Acyclic Graphs
- Running time : $\Theta(V+E)$
```pseudo
DAG-SHORTEST-PATHS(G,w,s)
1	topological sort the vertices of G
2	INITIALIZE-SINGLE-SOURCE(G,s)
3	for each vertex u, taken in topologically sorted order
4		for each vertex v ∈ G.Adj[u]
5			RELAX(u,v,w)
```
## Contents
%% Begin Waypoint %%
- [[Bellman-Ford Algorithm]]
- [[Breadth-First Search]]
- [[Depth-first Search]]
- [[Dijkstra Algorithm]]
- [[Floyd-Warshall Algorithm]]
- [[Topological Sort]]

%% End Waypoint %%