## Reference : [Search Algorithms in AI - GeeksforGeeks](https://www.geeksforgeeks.org/search-algorithms-in-ai/?ref=header_outind)
## Base
- Agent: An entitiy that perceives its enviroment and acts upon that environment.
- State: A configuration of the <font color="#92cddc">agent</font> and its <font color="#92cddc">environment</font>.
- Initial state: The state in which the agent begins
- Actions: choices that can be made in a state.
	- ACTION() returns the set of actions that can be executed in state .
- Transition model: describes what each action does.
	- RESULT(s, a) returns the state resulting from performing action in state .
	- ![](https://i.imgur.com/NWGeGlR.jpeg)
- State space : A set of possible _states_ that the environment can be in
- Goal test: A way to determine whether a given state is a goal state.
- Path cost: A numerical cost associated with a given path.
- Solution: A sequence of actions that leads from the initial state to a goal state.
- Optimal solution: A solution that has the lowest path cost among all solutions.

## Graph Search Problems (Uniformed)
![](https://i.imgur.com/4mXFnwO.jpeg)
-> It could be go wrong when repeat node exists. And not efficiency.
-> make an empty explored set which process already visited node
- Uniformed Search Algorithms
	- [[Depth-first Search|DFS]] (with stack)
	- [[Breadth-First Search|BFS]] (with queue)
- How can we make our search algorihm more intelligent
	- Informed  (Heuristic) Search

## Infomed Search Strategies
> A search strategy that use problem-specific knowledge to find solutions more efficiently than an uniformed strategy.
> Uses domain-specific hints about the location of goals

- The hints comes in the form of a heuristic function, denoted $h(n)$:
	- In route-finding problems, we can estimate the distance from the current state to a goal by computing the straight-line distance on the map btw two points.
	- $h(n)$ = estimated cost of the cheapest path from the state at node $n$ to a goal state. 

![](https://i.imgur.com/QGoKetE.png)
- Informed Search Algorithms 
	- [[Greedy Best-First Search]] : $h(n)$ = straight line distance to the goal
	- [[A-star Search]]