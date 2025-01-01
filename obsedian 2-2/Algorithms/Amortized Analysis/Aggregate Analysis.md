#algorithms 
## Aggregate analysis 
### 1. Example of stack operation
- Stack operations
	- PUSH(x)
	- POP() 
	- run in $O(1)$ time
	- MULTIPOP(k) : Actual running time is linear in the number of POP operations acutally executed
```pseudo
MULTIPOP(S,k)
1	while not STACK-EMPTY(S) and k > 0
2		POP(S)
3		k = k - 1
```

- Analysis of a sequence of n PUSH, POP and MULTIPOP operations
	- The worst-case of one MULTIPOP $O(n)$ ; stack size at most n
	- Total cost : $O(n^2)$
		- This cost isn't tight
	1. on an initially empty stack
	2. \[PUSH, PUSH, POP, PUSH, PUSH, PUSH, MULTIPOP(2), ...]
	=  \[PUSH, PUSH, POP, PUSH, PUSH, PUSH, {POP, POP}, ...] 
	$n\ \ \geq \#(PUSH) \geq \#(POP)$
	$2n\geq\#(PUSH)+\#(POP)$
	-> Total cost : $O(n)$
	- Amortized cost is $O(n) / n = O(1)$

### 2. Example of incrementing binary counter
```INCREMENT(A)
1	i = 0  \\ i is a bit index
2	while i < A.length and A[i] == 1
3		A[i] = 0
4		i = i + 1
5	if i < A.length
6	A[i] = 1	
```
- cost of INCREMENT oprations is proportional to the number of bits flip (3,6)
	- A single execution of INCREMENT takes time $\Theta(k)$ in the worst case
		- In which arrasy A contains all 1s.
		- Thus, a sequence of n INCREMENT oprations on an initially zero counter takes time $O(nk)$ in the worst case. 
	- Example of incrementing binary counter
		- Computing bit flip of Array A
			- Time of flip of A\[0] : $n$
			- Time of flip of A\[1] : $\lfloor n/2\rfloor$
			- Time of flip of A\[2] : $\lfloor n/4\rfloor$
		- The total number of flip in the sequence 
			- $\sum_{i=1}^{k-1}{\lfloor n/2^i\rfloor} <\sum_{i=0}^\infty{n/2^i} = 2n$
			- Total cost $O(n)$
		- Amortized cost = $O(n)/n = O(1)$
