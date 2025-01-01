#algorithms #graph #tree #bfs #stack
reference :
- [DFS 아카이브 - GeeksforGeeks](https://www.geeksforgeeks.org/tag/dfs/?ref=header_outind)
- Introductions to algorithms, 3rd
- [[Graph Basics]]
- [[Graph Representation]]

## Basic
![](https://i.imgur.com/59jowJR.png)
![](https://i.imgur.com/F5EJgqo.png)

## Depth-First Search
- The predecessor subgraph is a **depth-first forest**
- ***Parenthesis theorem (for gray interval)***
	- ***Inclusion*** : The ancestor's includes the descendants'
	- ***Disjoint*** : Otherwise
	- ![](https://i.imgur.com/xBBKfMY.png)
- Classification of edges
	- ![](https://i.imgur.com/FkE3Din.png)
	- Tree edges
	- Back edges (descendant -> ancestor)
	- Forward edges (ancestor -> descendant)
	- Cross edges (edges to other disjoint set)
- Classification by the DFS algorithm
	- Each edge $(u,v)$ can ve classified by the color of the vertex $v$ that is reached when the edges is first explored:
		- **white** indicates a tree edge,
		- **gray** indicates a back edge,
		- **black** indicates a forward or cross edge
	- Forward and cross edges are classified by ***the inclusion of gray intervals of u and v***
- In a depth-first search of an **undirected graph**, every edge of G is either a **tree edge**(cross edge) or a **back edge**(forward edge)

## Code
![](https://i.imgur.com/RUnR6Rd.png)
```pseudo
DFS(G)
1	for each vertex u ∈ G.V
2		u.color = WHITE
3		u.π = NIL
4	time = 0
5	for each vertex u ∈ G.V
6		if u.color == WHITE
7			DFS-VISIT(G,u)

DFS-VISIT(G,u)
1	time = time + 1
2	u.d = time
3	u.color = GRAY
4	for each v ∈ G.Adj[u]
5		if v.color == WHITE
6			v.π = u
7			DFS-VISIT(G,v)
8	u.color = BLACK
9	time = time + 1
10	u.f = time
```
- DFS : 1 ~ 4 ; Initialization $\Theta(V)$
- DFS : 5 ~ 7 ; Graph Exploration $\Theta(V+E)$
- DFS-Visit ($i$th call) $\Theta(Vi+Ei)$ 
## Complexity
- ### Running time
	- **Initialization** : $\Theta(V)$
	- **Exploring the graph** : $\Theta(V+E)$
	- **DFS-Visit** : $\Theta(Vi+Ei)$
		- undirected graph -> $i = 1$