#artificial_intelligence #algorithms 
## Ref 
- [A* Search Algorithm - GeeksforGeeks](https://www.geeksforgeeks.org/a-search-algorithm/?ref=gcse_outind)
- AIMA Book

## $A^*\ \text{Search}$
> A search algorithm that **expands the node with the lowest value of $g(n)+h(n)$**
> - $g(n)$ : the path cost from the initial state to node $n$
> - $h(n)$ : the _estimated_ cost of the shortest path from $n$ to a goal state

- ### The optimality
	- $A^*\ \text{(tree) search is (cost-)optimal if }h(n)\ \text{is admissible}$
		- An <font color="#de7802">admissible</font> heuristic is one that <font color="#fac08f">_never overestimates_ the cost to reach a goal.</font> 
		- An admissible heuristic is therefore <font color="#fac08f">optimistic</font>.
		- Formally, given $h^*(n)$ which is the cost of the optimal path from $n$ to the nearest goal, we have: $$h(n)\leq h^*(n)$$
	- Proof (by contradiction)
		- Suppose the optimal path has cost $C^*$, but the algorithm returns a path with cost $C>C^∗$.
		- Then there must be some node which is on the optimal path and is **unexpanded (i.e., unvisited)** (because if all the nodes on the optimal path had been expanded, then we would have return that optimal solution).
		- So then, using the notation $g^∗(n)$ to mean **the cost of the optimal path from the start to $n$** , and $h^∗(n)$ to mean **the cost of the optimal path from $n$ to the nearest goal**, we have: $$\begin{align}(1)\ &f(n) > C^*\ \text{otherwise n would have been expanded}  \\ (2)\ &f(n) = g(n) + h(n)\ \text{(by definition)} \\ &f(n) = g^*(n) + h(n)\ \text{(because n is on an optimal path)}\\ &f(n)\leq g^*(n) + h^*(n)\ \text{(because fo admissibility, }h(n)\leq h^*(n))\\ &f(n) \leq C^*\ \text{(by definition, }C^*=g^*(n)+h^*(n))\\ &\qquad\qquad\qquad\therefore C = C^*\end{align}$$
- ### heuristic function $h(n)$
	- In practical scenarios, we generally do <font color="#fac08f">not</font> have enough information to specify a good heuristic function or approximator 
