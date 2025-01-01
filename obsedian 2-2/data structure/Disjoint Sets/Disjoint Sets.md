 #datastructure #algorithms #disjoint_set 

## Disjoint Sets
- Two sets $A$ and $B$ are disjoint if $A\cap B =\emptyset$
- Sets $S_1,S_2,\cdots,S_k$ are disjoint if every two disjoint sets  $S_i$ and $S_j$ are disjoint
- A ***collection*** of disjoint sets
	- A set of disjoint sets is called a collection of disjoint sets
	- Each set in a collection has a *representative member* and the set is identified by the member

## Types
- Array representation (Similar to Forest)
- [[Disjoint Sets (Linked List)|Linked List representation]]
- [[Disjoint Sets (Forest)|Forest representation]]

## [[Operation of Disjoint Sets|Operation]]

| Basic Operation | Time | Space |
| --------------- | ---- | ----- |
| Make-set        |      |       | 
| Union           |      |       |
| Find            |      |       |
| Build           |      |       |

## [[Optimization of Disjoint Sets|Optimization]]

## Application of Disjoint Sets
- #### Computing connected components ([[Connected Component|CC]])
	- Static Graph
		- Depth-first  search : $\Theta(V+E)$
	- Dynamic Graph
		- Depth-first search is inefficient
		- Maintaing a disjoint-set data structure is more efficient

### Contents
%% Begin Waypoint %%
- [[Disjoint Sets (Forest)]]
- [[Disjoint Sets (Linked List)]]
- [[Operation of Disjoint Sets]]
- [[Optimization of Disjoint Sets]]

%% End Waypoint %%