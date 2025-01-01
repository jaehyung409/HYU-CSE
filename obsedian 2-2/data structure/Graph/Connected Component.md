#graph 
### Ref : 
- [[알고리즘] 그래프 (3) - 연결 요소(Connected Components)와 단절점(Articulation Point) — Shin._.Mallang](https://ttl-blog.tistory.com/956)

> Connected Component G' of G : Maximal connected subgraph of G (induced subgraph)

### [[Depth-first Search]] : $\Theta(V+E)$
### [[Disjoint Sets]] : $UNION(h,j)$
![](https://i.imgur.com/HigXG0b.png)
```pseudo
CONNECTED-COMPONENTS(G)
1	for each vertex v ∈ G.V
2		MAKE-SET(v)
3	for each edge (u,v) ∈ G.E
4		if FIND-SET(u) != FIND-SET(v)
5			UNION(u,v)

SAME-COMPONENT(u,v)
1	if FIND-SET(u) == FIND-SET(v)
2		return TRUE
3	else return FALSE
```
