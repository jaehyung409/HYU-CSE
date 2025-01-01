## The Bellman-Ford Algorith
- It solves the single source shortest-paths problem in the <font color="#fac08f">general case in which edge weights may be negative</font>

## Code
```pseudo
BELLMAN-FORD(G,w,s)
1	INITIALIZE-SINGLE-SOURCE(G,s)
2	for i = 1 to |G.V|-1
3		for each edge(u,v) ∈ G.E
4			RELAX(u,v,w)
5	for each edge(u,v) ∈ G.E
6		if v.d > u.d + w(u,v)
7			return FALSE
8	return TRUE
```
## Complexity
- line 3 ~ 4 : $V *\Theta(E)$
- line 5 ~ 7 : $\Theta(E)$
- Total : $\Theta(VE)$