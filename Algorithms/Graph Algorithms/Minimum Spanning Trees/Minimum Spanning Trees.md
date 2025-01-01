#mst #algorithms #tree #graph 
## Minimum Spanning Trees Problem
- Finding a spanning tree whose cost is the smallest
- $T$ is acyclic and connects all of vertices $\rightarrow$ a tree
#### Generic-MST
```pseudo
GENERIC=MST(G,w)
	A = {}
	while A does not form a spanning tree
		do find an edge (u,v) that is safe for A
		A = A ∪ {(u,v)}
	return A
```
- It grows the minimum spanning tree one edge at a time
- It adds an edge $(u,v)$ to A such that $A\cup{(u,v)}$ is also a subset of some minimum spanning tree
	- Call such an edge a ***safe edge*** for $A$
## Contents
%% Begin Waypoint %%
- [[Kruskal Algorithm]]
- [[Prim Algorithm]]

%% End Waypoint %%
