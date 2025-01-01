#dp #algorithms
reference : 
- [매트릭스 체인 곱셈 - GeeksforGeeks](https://www.geeksforgeeks.org/matrix-chain-multiplication-dp-8/?ref=header_outind)
- Introductions to algorithms, 3rd

### Problems
> Given a chain $A_1, A_2, ..., A_n\ \text{of } n$ matrices, where matrix $A_i$ has dimension $p_{i-1} \times p_i$, find the order of matrix multiplications minimizing the scalar multiplications to compute the product
> That is, to fully parenthesize the product of matrices minimizing scalar
> $A_1:p_0\times p_1, A_2:p_1\times p_2, A_3:p_2\times p_3\ ...$ 
##### Basics
- Multiplying two matrices A and B
	- A (p x q) and B (q x r) can be multiplied
	- \# of scalar multiplication is *pqr*
- $(A_1 \cdot A_2)\cdot A_3 = A_1\cdot (A_2\cdot A_3)$

### Brute force approach
$$P(n) = \begin{cases}1&\text{if } n = 1 
\\ \sum_{k=1}^{n-1}{P(k)P(n-k)}&\text{if } n\geq 2\end{cases}$$
- The \# of enumerated parenthesizeations is $\Omega(4^n/n^{3/2})$, inefficient
### Dynamic Programing
- Optimal substructure
	- $m[i][j]$ : The minimum \# of scalar multiplications for computing $A_i,A_{i+1}, ... ,A_j$
	- $$m[i][j] = \begin{cases}0&\text{if }i=j \\ min_{i\leq k<j}\{m[i][k] + m[k+1][j] + p_{i-1}p_kp_j\} &\text{if }i<j \end{cases}$$
	- matrix $A_i: p_{i-1}\times p_i$
	- computing $A_{i..k}A_{k+1..j}\text{takes }p_{i-1}p_kp_j$ scalar multiplications
	- $s[i][j]$ stores the optimal <font color="#e36c09">$k$</font> for tracing the optimal solution

| i\\j | 1                              | 2                                                    | 3                                       | 4          | 5          | 6          |
| ---- | ------------------------------ | ---------------------------------------------------- | --------------------------------------- | ---------- | ---------- | ---------- |
| 1    | <font color="#e36c09">0</font> | <font color="#ff0000">$\Pi_{k=i-1}^{j}{P(k)}$</font> |         m[1][3]                                |            |            |            |
| 2    |                                | 0                                                    | <font color="#e36c09">$\nwarrow$</font> |            |            |            |
| 3    |                                |                                                      | <font color="#ff0000">0  </font>                                     | $\nwarrow$ |            |            |
| 4    |                                |                                                      |                                         | 0          | $\nwarrow$ |            |
| 5    |                                |                                                      |                                         |            | 0          | $\nwarrow$ |
| 6    |                                |                                                      |                                         |            |            | 0          |
- m\[1]\[3] = min(<font color="#e36c09">val + p(i-1)p(k)p(j)</font> , <font color="#ff0000">val + p(i-1)p(k)p(j)</font>) , k = colum of selected, which not j
```pseudo
MATRIX-CHAIN-ORDER(p)
1	n = p.length - 1
2	let m[1..n][1..n] and s[1..n-1][2..n] be new tables
3	for i = 1 to n
4		m[i][i] = 0
5	for l = 2 to n
6		for i = 1 to n - l + 1
7			j = i + l - 1
8			m[i][j] = ∞
9			for k = i to j - 1
10			    q = m[i][k] + m[k+1][j] + p[i-1]p[k]p[j]
11			    if q < m[i][j]
12				    m[i][j] = q
13				    s[i][j] = k
14	return m and s

PRINT-OPTIMAL-PARENS(s,i,j)
1	if i == j
2		print "A[i]"
3	else print "("
4		PRINT-OPTIMAL-PARENS(s,i,s[i][j])
5		PRINT-OPTIMAL-PARENS(s,s[i][j] + 1,j)
6	print ")"
```

### Performance
- Space consumption
	- Table m : $n^2$
	- Table s : $n^2$
	- $\Theta(n^2)$ elements in total                                                                                                   
- Running time
	- $$\begin{align}&1\cdot n + 1\cdot n-1 + 2\cdot n-2 + ... + n-1\cdot1 &&
	\\ &=1\cdot n + \sum_{k=1}^{n-1}{k(n-k)} &&
	\\ &=1\cdot n + \sum{k=1}^{n-1}{kn}-\sum_{k=1}^{n-1}{k^2} &&
	\\ &=n + n^2(n-1)/2-n(n-1)(2n-1)/6 &&
	\\ &=n^3 + 5n/6 &&
	\\ &=\Theta(n^3) && \end{align}$$
	- $\Theta(n^3)$ time in total

- Table $r$ can be reduced like table $s$ in [[Assembly-line Scheduling#^0bd1f9|Assembly-line Scheduling]]?
	- No. It needs all previous results.


