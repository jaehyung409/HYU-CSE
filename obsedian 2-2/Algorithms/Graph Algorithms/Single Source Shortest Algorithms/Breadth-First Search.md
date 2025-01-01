#algorithms #graph #tree #bfs #queue
reference :
- [BFS 아카이브 - GeeksforGeeks](https://www.geeksforgeeks.org/tag/bfs/)
- Introductions to algorithms, 3rd
- [[Graph Basics]]
- [[Graph Representation]]

## Breadth-First Search
- Given a graph $G=(V,E)$ and a ***source*** vertex *s*, it explores the edges of *G* to "discover" every reachable vertex from *s*
- It discovers vertices in the increasing order of distance from the source. It first discovers all vertices at distance 1, then 2, and etc.
- It also computes
	- The distance of vertices from the source : $u.d$
	- The predecessor of vertices : $u.\pi$
- The ***predecessor subgraph*** of $G$ as $G_{\pi}=(V_{\pi},E_{\pi})$		
	- $V_{\pi}=\{v\in V:v.\pi\neq NIL\}\cup \{s\}$
	- $E_{\pi}=\{(v.\pi,v):v\in V_{\pi} - \{s\}\}$
	- The predecessor subgraph $G_{\pi}$ is a **breadth-first tree**
		- since it is connected and $|E_{\pi}|=|V_{\pi}|-1$
		- The edges in $E_{\pi}$ are called ***tree edges***

## Code
![](https://i.imgur.com/YBFay1G.png)
```pseudo
BFS(G,s)
1	for each vertex u ∈ G.V - {s}
2		u.color = WHITE
3		u.d = ∞
4		u.π = NIL
5	s.color = GRAY
6	s.d = 0
7	s.π= NIL
8	Q = {}
9	ENQUEUE(Q,s)
10	while Q ≠ {}
11		u = DEQUEUE(Q)
12		for each v ∈ G.Adj[u]
13			if v.color == White
14				v.color = GRAY
15				v.d = u.d + 1
16				v.π = u
17				ENQUEUE(Q,v)
18		u.color = BLACK
```
- Part 1 (1 ~ 9) : Initialization $\Theta(V)$
- Part 2 (10 ~ 18) : Graph Exploration $O(V+E)$
- Is Coloring necessary ?
	- Delete all color line (2,5,14,18)
	- Modify line 7 `s.π = s`
	- Modify line 13 `v.d == ∞` or `v.π == NIL`
	- Or Using visited array

## Complexity
- ### Running time
	- **Initialization** : $\Theta(V)$
	- **Exploring the graph** : $O(V+E)$
		- A vertex is examined at most once.
		- An edge is explored at most twice.
			- undirected : twice
			- directed : once
	- **Overall** : O(V+E)