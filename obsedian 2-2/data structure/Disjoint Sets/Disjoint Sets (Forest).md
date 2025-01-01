#disjoint_set #tree #datastructure
## Disjoint Sets (Forest)
![](https://i.imgur.com/qtqCy9Y.png)
## Operations & Optimization
```pseudo
MAKE-SET(x)
1	x.p = x

FIND-SET(x)
1	if x == x.p
2		return x
3	else return FIND-SET(x. p)
```
- Union by rank
	- **idea** : Attach the shorter tree to the higher tree
	- Each node maintains a ***rank***, which is an upper bound on the height of the node
	- Compare the ranks of the two roots and attach the tree whose root's rank is smaller to the other 
```
MAKE-SET(x)
1	x.p = x
2	x.rank = 0

UNION(x)
1	LINK(FIND-SET(x), FIND-SET(x))

LINK(x,y)
1	if x.rank > y.rank
2		y.p = x
3	else x.p = y
4		if x.rank == y.rank
5			y.rank = y.rank + 1
```
- Path compression 
	- Change the parent to the root during FIND-SET(x)
```
FIND-SET(x) 
	if x != x.p
		x.p = FIND-SET(x.p)
	return x.p
```
## Running time for BUILD (rank, path compression)
- Worst case running time : $O(m\alpha(n))$
- $\alpha(n)\leq4$ : for all practical situations 
