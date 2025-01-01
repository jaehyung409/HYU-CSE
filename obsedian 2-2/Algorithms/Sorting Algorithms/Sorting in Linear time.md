#algorithms #sorting 

## Lower Bounds for Sorting
- Ref : [비교 기반 정렬 알고리즘의 하한 - GeeksforGeeks](https://www.geeksforgeeks.org/lower-bound-on-comparison-based-sorting-algorithms/)
- ### Compariosn Sorts
	- Basic :
		- Distinct element
		- all comparisions have the form of $a_i \leq a_j$
	- Heapsort, Mergesort, Insertion sort, Selection sort, Quicksort
	- $\Omega(n\lg n)$
	- decision-tree model ![](https://media.geeksforgeeks.org/wp-content/uploads/20230315121139/Screenshot_20230315_115855.png)
		- left subtree : $x \leq y$ , right subtree : $x \geq y$
		- The worst-case number of comparisons = the height of its decision tree
		- Proof : $$\begin{align}The\ number\ of\ leaves &= n!
		\\ n! &\leq 2^h
		\\\lg(n!) &\leq h
		\\&\ \therefore \Omega(n\lg n)
		\end{align}$$

## Counting Sort![[Counting sort]]
## Radix Sort![[Radix Sort]]