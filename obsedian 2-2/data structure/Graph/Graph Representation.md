### Adjacency-list representation 
- $\Theta(V+E)$ space
- An array of $|V|$ lists, one for each vertax
- For vertax *u*, its adjacency list contains all vertices adjacent to *u*
	- ![](https://i.imgur.com/Z18AIT4.png)
- For an undircted graph, its directed version is stored.
	- ![](https://i.imgur.com/cMBeN7w.png)

### Adjacency-matrix representaion
- $|V|\times|V|$ matrix : $\Theta(O^2)$ space
- Entry $(i,j)$ is 1 if there is an edge and 0 otherwise
	- ![](https://i.imgur.com/fXpBf6s.png)
- For an undirected graph, there is a symmetry along the main diagonal of its adjacency matrix
- Storing the lower matrix is enough
	- ![](https://i.imgur.com/PwkGJBH.png)




### Comparision of adjacency list an adjacency matrix
- Storage
	- If *G* is sparse, adjacency list is better
		- because $|E| < |V|^2$
	- If *G* is dense, adjacency matrix is better
		- because adjacency matrix tries use only one bit for an entry
- Edge present test : does an edge $(i,j)$ exist?
	- Adjacency matrix : $\Theta(1)$ time
	- Adjacency list : $O(V)$ time
- Listing or visiting all edges
	- Adjacency matrix : $\Theta(V^2)$ time
	- Adjacency list : $\Theta(V+E)$ time

### Weighted graph representation
> Edges have weights
- ![](https://i.imgur.com/4N6Es3F.png)
- ![](https://i.imgur.com/A9bNoL7.png)
