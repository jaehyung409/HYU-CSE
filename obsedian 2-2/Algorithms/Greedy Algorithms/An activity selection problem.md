#greedy #algorithms 

reference : 
- [Activity Selection Problem | Greedy Algo-1 - GeeksforGeeks](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/?ref=gcse_outind)
- Introductions to algorithms, 3rd

### Problems
![](https://media.geeksforgeeks.org/wp-content/uploads/20240716144640/Activity-Selection-Problem-0.webp)
- To select a maximum-size subset of mutually compatible activities
	- Given *n* classes and 1 lecture room
	- to select the maximum number of classes
- A set of _activities_: S = {$a_1, a_2, ..., a_n$}
- Each activity $a_i$ has its **start time $s_i$** and **finish time $f_i$**
	- $0\leq s_i < f_i < \infty$
- Activity $a_i$ takes placce during \[$s_p,f_i$)
- Activities $a_i$ and $a_j$ are **compeatible** if the intervals \[$s_p,f_i$) and \[$s_j,f_j$) do not overlap

### Greedy Algorithms
- ##### Optimal substructure
	- Assume that activities are sorted in increasing order of finish tiem
	- $$f_0\leq f_1\leq f_2\leq ... \leq f_n < f_{n+1}$$
- ##### Greedy algorithm
	- Select the earliest finishing activity one by on

### Performance
- Space consumption
	- $O(1)$
- Time complexity
	- $O(N \lg N)$ for sorting, $O(N)$ for selecting                                                                                                  