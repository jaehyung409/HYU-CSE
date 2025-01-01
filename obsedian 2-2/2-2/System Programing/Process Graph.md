## Process Graph
- A ***process graph*** is a useful tool for capturing the partial ordering of statements in a concurrent program
	- Each vertex is the execution of a statement
	- <font color="#fac08f">a $\rightarrow$ b</font> means <font color="#fac08f">a</font> happens before <font color="#fac08f">b</font>
	- Edges can be labeled with current value of variables
	- $\text{printf}$ vertices can be labeled with output
	- Each graph begins with a vertex with no inedges
- Any [[Topological Sort]] of the graph corresponds to a feasible total ordering
	- Total oredering of vertices where all edges point from left to right