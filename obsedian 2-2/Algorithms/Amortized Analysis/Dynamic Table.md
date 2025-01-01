#algorithms 
### Dynamic Table
> Table allocation problem
> - Insertion(expansion) : So allocate space for a table and reallocate the table when new item is added
> - Deletion(contraction) : Similarly, if many objects have been deleted from the table, it may be worthwhile to reallocate the table with a smaller size 
Using amortized analysis, we shall show that the amortized cost of insertion and deletion is only $O(1)$
### Insertion (Expansion)
```pseudo
TABLE-INSERT(T,x)
1	if T.size == 0
2		allocate T.table with 1 slot
3		T.size = 1
4	if T.num == T.size
5		allocate new-table with 2 * T.size slots
6		insert all items in T.table into new-table
7		free T.table
8		T.table = new-table
9		T.size = 2 * T.size
10	intset x into T.table
11	T.num = T.num + 1
```

#### Aggregate analysis
- Let us analyze a sequence of *n* TABLE-INSERT operations on an initially empty table.$$c_i=\begin{cases}i &\text{if i - 1 is an exact power of 2}\\1 &\text{otherwise}\end{cases}$$
- The total cost of n TABLE-INSERT operations Is therfore $$\begin{align}\sum_{i=1}^n{c_i} &\leq n +\sum_{j=0}^{\lfloor\lg n\rfloor}{2^j} \\&< n+2n \\ &= 3n \end{align}$$
#### Accounting method
- each item pays for 3 elementary insertions :
	- 1 **cost** for line 10
	- 2 **credit** for line 6
		- moving itself when the table expands
		- moving another item that has already been moved once when the table expands
	- Credit is used to move items when expansion occurs
#### Potential method
- $\Phi(T) = 2*T.num - T.size$, always nonnegative
- $\hat{c}_i = 3$

### Deletion (Contraction)
- load factor : $\alpha(T) = T.num/T.size$
- When we apply table contraction, we would like to preserve two properties :
	- The load factor of the table is ***bounded below*** by a positive constant
	- The amortized cost of a table operation is ***bounded above*** by a constant.
- A simple strategy for table contraction
	- We double the table size before we insert an item into a full table.
	- We halve the table size if the table is less than half full after deletion
	- This strategy guarantees that the load factor is at least 1/2, but ***the amoritzed cost is quite large***, $\Theta(n^2)$ : ( n/2 -> insert delete delete .... )
		- We halve the table size after we delete an item if the table is less than 1/4 full
#### Potential method
$\alpha(T) = T.num/T.size$, If *T* is empty, $\alpha(T) = 1$
- $$\Phi_i=\begin{cases}2 * num_i - size_i&\text{if }\alpha(T)\geq1/2 \\ size_i/2-num_i&\text{if }\alpha(T)<1/2\end{cases}$$
- TABLE-INSERT $O(1)$
	- Case 1 : $\alpha_{i-1} \geq 1/2$
		- Amortized cost is at most 3
		- which is explained in the table extension only case.
	- Case 2 : $\alpha_{i-1} < 1/2$
		- Case 2-1 : $\alpha_i < 1/2$
			- Then $size_i=size_{i-1}$, $num_{i-1}=num_i-1$
			- $$\begin{align}\hat{c}_i &= c_i +\Phi_i - \Phi_{i-1}\\&=1+(size_i/2-num_i)-(size_{i-1}/2-num_{i-1})\\&=1+(size_i/2-num_i)-(size_{i-1}/2-(num_i-1))\\&=0\end{align}$$
		- Case 2-2 : $\alpha_i \geq 1/2$ 
			- $$\begin{align}\hat{c}_i&=c_i+\Phi_i-\Phi_{i-1}\\&=1+(2*num_i-size_i)-(size_{i-1}/2-num_{i-1})\\&=1+(2*(num_{i-1}+1)-size_{i-1})-(size_{i-1}/2+num_{i-1})\\&=3*num_{i-1}-3size_{i-1}/2+3\\&=3\alpha_{i-1}size_{i-1}-3size_{i-1}/2+3\qquad(num_i=\alpha_i*size)\\&<3size_{i-1}/2-3size_{i-1}/2+3\qquad\quad(\alpha_{i-1}<1/2)\\&=3\end{align}$$
	- Thus, the amortized cost of a TABLE-INSERT operationsa is at most 3 
- TABLE-DELETE $O(1)$
	- $num_i = num_{i-1} - 1$
	- If $a_{i-1}<1/2$, the *j*th operations causes
		- no contraction ($size_i=size_{i-1}$)
			- $$\begin{align}\hat{c}_i&=c_i+\Phi_i-\Phi_{i-1}\\&=1+(size_i/2-num_i)-(size_{i-1}/2-num_{i-1})\\&=1+(size_i/2-num_i)-(size_i/2-(num_i+1))\\&=2\end{align}$$
		- contraction
			- actual cost of the operation is $c_i = num_i + 1$
			- $size_i/2=size_{i-1}/4=num_{i-1}=num_i+1$
			- $$\begin{align}\hat{c}_i&=c_i+\Phi_i-\Phi_{i-1}\\&=(num_i+1)+(size_i/2-num_i)-(size_{i-1}/2-num_{i-1})\\&=(num_i+1)+((num_i+1)-num_i)-((2*num_i+2)-(num_i+1))\\&=1\end{align}$$
	- If $a_{i-1}\geq1/2$
		-  it's amortized cost is constant