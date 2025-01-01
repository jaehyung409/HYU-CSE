#greedy #algorithms
#### Ref 
- [Greedy Algorithms - GeeksforGeeks](https://www.geeksforgeeks.org/greedy-algorithms/?ref=header_outind)
- [Greedy Algorithms (General Structure and Applications) - GeeksforGeeks](https://www.geeksforgeeks.org/greedy-algorithms-general-structure-and-applications/?ref=gcse_outind)
- [Greedy Algorithm Tutorial - Examples, Application and Practice Problem - GeeksforGeeks](https://www.geeksforgeeks.org/introduction-to-greedy-algorithm-data-structures-and-algorithm-tutorials/?ref=header_outind)
- Introductions to algorithms, 3rd
### Greedy
- A **greedy algorithm** always make the choic that looks best at the moment
- It makes a locally optimal choice in the hope that this choice will lead to a globally optimal solution
- It makes the choice *before* the subproblems are solved

### Examples
- [[An activity selection problem]]
- [[Huffman Codes]]

### Elements of the greedy strategy
- Greedy-choice property
	- Make the choice _**before**_ the subproblems are solved
	- Only one subproblem is generated
- Dynamic programing
	- Make a choice _**after**_ the subproblems are solved.
	- Several subproblems may be generated.
- Greedy vs. Dynamic programing ^72d797
	- [Difference Between Greedy Knapsack and 0/1 Knapsack Algorithms - GeeksforGeeks](https://www.geeksforgeeks.org/difference-between-greedy-knapsack-and-0-1-knapsack-algorithms/?ref=oin_asr1)
	- 0-1 knapsack
		- A thief robbing a store finds _n_ items.
		- The $i$th item is worth $v_i$dollars and weighs $w_i$ pounds.
		- He can carry at most $W$ pounds in his knapsack.
		- The $n, v_i, w_i, \text{and } W$ are integers.
		- Which items should he take?
			- The DP works.
	- Fractional knapsack
		- In this case, the thief can take fractions of items
			- The greedy strategy works
			- Compute the value per pound $v_i/w_i$ for each itme
			- Take as much as possible of the item with the greatest value per pound 

