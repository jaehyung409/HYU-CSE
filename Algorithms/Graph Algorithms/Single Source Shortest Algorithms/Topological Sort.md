#topological_sorting 
### Ref :
- [Topological Sorting - GeeksforGeeks](https://www.geeksforgeeks.org/topological-sorting/?ref=gcse_outind)

### Topological Sorting
> Given a DAG (directed acyclic graph), generate a linear ordering of all its vertices such that all edges go from left to right
#### Indegree Array (with Stack or Queue)
1. Make Indegree Array
2. indegree == 0 : push element to Stack or Queue structure.
3. pop element from Stack or Queue. and print it.
4. eliminate all edges from element node, and reduce Indegree Array's value
5. If another value go to 0, Push it.
6. Iteratively when Stack or Queue is empty (Done!)
- Time Complexity : $\Theta(V+E)$
#### Using [[Depth-first Search]]
- **Main ideas**
	- Successively place a node from the *left* with *0 in-degree*
	- Successively place a node from the *right* with *0 out-degree*
	- Run DFS on G and place the nodes from the *right* in the *increasing order of the finishing time*
	- (Think of Gray Interval)
- Time Complexity : $\Theta(V+E)$
- Correctness
	- If there is an edge from $u$ to $v$, then $v.f < u.f$
	- A directed graph G is **acyclic** if and only if a depth-first search of G yields **no back edges**

#### Cycle ..?