#algorithms 
## Recurrence
- When an algorithm contains a recursive call to itself, its running time can often by a recurrence.
- A recurrence is an equation or inequality that describes a function in terms of its value on smaller inputs
- Three methods for solving recurrences
	- Substitution method
	- Recursion-tree method
	- Master method
 
### Substition method
1. Guess the solution
2. Use mathematical induction to prove the guess is right
	- Basis or boundary conditions
	- Inductive step

### Recursion-tree method
ref : [재귀 트리 방법을 사용하여 시간 복잡도 재귀 관계를 해결하는 방법은 무엇입니까? - GeeksforGeeks](https://www.geeksforgeeks.org/how-to-solve-time-complexity-recurrence-relations-using-recursion-tree-method/)
1. Draw a recursive tree
2. Calculate the cost at each level and count the total no of levels in the recursion tree
3. Count the total number of nodes in the last level and calculate the cost of the last level
4. Sum up the cost of all the levels in the recursive tree