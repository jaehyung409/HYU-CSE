#graph #algorithms 
## Ref
- [Floyd Warshall Algorithm - GeeksforGeeks](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/?ref=gcse_outind)
## Definition
- Adjacency Matrix $W$
	- $w_{ij}=w(i,j)$, No-edge : $\infty$
- Shortest Distance Matrix $D$
	- $d_{ij}=\delta(i,j)$
	- Distance = Path\_Cost($\sum^{(j\rightarrow\pi_{ij})=i}\pi_{ij}\rightarrow j$)
- Predecessor Matrix $Pi$
	- $\pi_{ij}=NIL$ if either $i=j$ or there is not path from $i$ to $j$
	- $\pi_{ij}$ is the predecessor of $j$ on some shortest path from $i$ to $j$
```pseudo
PRINT-ALL-PAIRS-SHORTEST-PATH(П,i,j)
1	if i == j
2		print i
3	elseif π[i][j] == NIL
4		print "no path from" i "to" j "exists"
5	else PRINT-ALL-PAIRS-SHORTEST-PATH(П,i,π[i][j])
6		print j
```

## Floyd-Warshall algorithm, $\Theta(n^3)$
- Intermediate Vertex
	- An intermediate vertex of a simple path $p=<v_1,v_2,\cdots,v_l>$ is any vertex of $p$ between $v_1$ and $v_j$
- The structure of a shortest path 
	- Floyd-Warshall algorithm is based on the observation of the intermediate vertives, which costs $\Theta(V^3)$ time
	- Let $V=\{1,2,\cdots,n\}$
	- For any pair of vertices $i,j\in V$, consider all paths from $i$ to $j$ whose intermediate vertices are all drawn from $\{1,2,\cdots,k\}$, and let $p$ be a minimum weight path from among them
		- If $k$ is not an intermediate vertex of path $p$, then all intermediate vertices of $p$ are in $\{1,2,\cdots,k-1\}$
		- If $k$ is an intermediate vertex of path $p$, then we break $p$ down into $i\rightarrow k\rightarrow j$![](https://media.geeksforgeeks.org/wp-content/uploads/dpFloyd-Warshall-.jpg)
	- *TIp. treat $k$ as a stage, $\{1,2,\cdots,k-1\} = (k-1)_{th}$*
- A recursive solution to the all-pairs shortest-paths problem
	- Let $d_{ij}^{(k)}$ be the weight of a shortest path from vertex $i$ to vertex $j$ for which all intermediate vertices are in the set$\{1,2,\cdots,k\}$
	- We have the following recurrence$$d_{ij}^{(k)}=\begin{cases}w_{ij}&\text{if }k=0\\ min(d_{ij}^{(k-1)},d_{ik}^{(k-1)}+d_{kj}^{(k-1)}&\text{if }k\geq1\end{cases}$$
	- Because for any path, all intermediate vertices are in the set $\{1,2,\cdots,n\}$, the matrix $D^{(n)}=d_{ij}^{(n)}$ gives the final answer 
		- $d_{ij}^{(n)}=\delta(i,j)$ for all $i,j\in V$
```pseudo
FLOYD-WARSHALL(W)
1	n = W.rows
2	D[0] = W
3	for k = 1 to n
4		let D[k] = (d[k][i][j]) be a new n x n matrix
5		for i = 1 to n
6			for j = 1 to n
7				d[k][i][j] = min(d[k-1][i][j], d[k-1][i][k]+d[k-1][k][j])
8	return D[n]
```
- Constructing A Shortest Path
	- Let $\Pi_{ij}^k$ be the predecessor of vertex $j$ on a shortest path form vertex $i$ with all intermediate veritces in ${1,2,\cdots,k}$$$\begin{align}\Pi_{ij}^{(0)}&=\begin{cases}NIL&\text{if }i=j\ \text{or }w_{ij}=\infty\\i&\text{if }i\neq j\ \text{and }w_{ij}<\infty\end{cases}\\\Pi_{ij}^{(k)}&=\begin{cases}\Pi_{ij}^{(k-1)}&\text{if }d_{ij}^{(k-1)}\leq d_{ik}^{(k-1)}+d_{kj}^{(k-1)}\\\Pi_{kj}^{(k-1)}&\text{if }d_{ij}^{(k-1)}>d_{ik}^{(k-1)}+d_{kj}^{(k-1)}\end{cases}\end{align}$$
	- Simply, Changed Value of Shortest Path cost
		- set $\Pi_{kj}^{(k-1)}$