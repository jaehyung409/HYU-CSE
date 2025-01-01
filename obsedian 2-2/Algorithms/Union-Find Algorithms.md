#algorithms #disjoint_set #tree 
## [[Disjoint Sets]]
## Union-Find Algorithms
- same root value -> same set (Find)
	- Path compression (Find)
```pseudo
FIND-ROOT(x)
	if (x == parent[x]) return x;
	return parent[x] = FIND-ROOT(parent[x])
```
- different root value -> Different set (Union)
	- Optimization (Union by Rank)
```pseudo
UNION-ROOT(x,y)
	x = FIND-ROOT(x)
	y = FIND-ROOT(y)
	if (x != y) {
	// node-rank[x] : tree height (contain x)
		if (node_rank[x] < node_rank[y]) parent[x] = y;
		else parent[y] = x;
		if (node_rank[x] == node_rank[y]) {
			parent[x] = y;
			node_rank[x]++;
		}
	}
```