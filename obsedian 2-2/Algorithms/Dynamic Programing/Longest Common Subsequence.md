#dp #algorithms 
reference : 
- [가장 긴 공통 부분 시퀀스(LCS) - GeeksforGeeks](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/?ref=header_outind)
- Introductions to algorithms, 3rd

### Definition
- Character
- String (or Sequence) : A list of characters
	- ex> strings over {0, 1} : Binary strings
	- ex> strings over {A, C, G, T} : DNA sequences
- Substring
	- CBD is a substring of AB<font color="#e36c09">CBD</font>AB
- Subsequence
	- BCDB is a subsequence of A<font color="#e36c09">BC</font>B<font color="#e36c09">D</font>A<font color="#e36c09">B</font>
- Common Subsequence
	- BCA is a common subsequence of 
		- X = A<font color="#e36c09">BC</font>BD<font color="#e36c09">A</font>B
		- Y = <font color="#e36c09">B</font>D<font color="#e36c09">CA</font>BA
- LCS (Longest Common Subsequence)

### Brute force approach
- Enumerate all subsequences of X and check each subsequence if it is also a subsequence of Y and find the longest one.
- Infeasilbe!
	- The number of subsequence of X is $2^M$

### Dynamic Programing
- The $i$th $prefix\ X_i\ of X$ is $X_i =x_1x_2...x_i$
- If $X = ABCBDAB$
	- $X_4=ABCB$
	- $X_0=$
![](https://media.geeksforgeeks.org/wp-content/uploads/20240806161758/Longest-Common-Subsequence.webp)
1. If $x_m = y_n$ , then $z_k=x_m=y_n$ and $Z_{k-1}$ is an LCS of $X_{m-1}$ and $Y_{n-1}$
2. If $x_m \neq y_n$ , $Z$ is an LCS of $X_{m-1}$ and $Y$ or an LCS of $X$ and $Y_{n-1}$
- $c[i][j]$ : The length of LCS of the sequences $X_i$ and $Y_j$
$$c[i][j] = \begin{cases}0&\text{if } i = 0 \ \text{or } j = 0, 
\\ c[i-1][j-1] + 1 &\text{if } i,j > 0\ \text{and } x_i = y_j,
\\ max(c[i][j-1], c[i-1][j])&\text{if } i,j > 0\ \text{and } x_i \neq y_j
\end{cases}$$
![](https://media.geeksforgeeks.org/wp-content/uploads/20240718100203/Longest-Common-Subsequence-3.webp)

|     | j     | 0                              | 1                                        | 2                                          | 3                                        | 4                                          | 5                                          | 6                                         |
| --- | ----- | ------------------------------ | ---------------------------------------- | ------------------------------------------ | ---------------------------------------- | ------------------------------------------ | ------------------------------------------ | ----------------------------------------- |
| i   |       | $y_i$                          | B                                        | D                                          | C                                        | A                                          | B                                          | A                                         |
| 1   | $x_i$ | 0                              | 0                                        | 0                                          | 0                                        | 0                                          | 0                                          | 0                                         |
| 0   | A     | <font color="#e36c09">0</font> | 0                                        | 0                                          | 0                                        | 1$\nwarrow$                                | 1                                          | 1$\nwarrow$                               |
| 2   | B     | 0                              | <font color="#e36c09">1$\nwarrow$</font> | <font color="#e36c09">1$\leftarrow$</font> | 1$\leftarrow$                            | 1                                          | 2$\nwarrow$                                | 2$\leftarrow$                             |
| 3   | C     | 0                              | 1$\uparrow$                              | 1                                          | <font color="#e36c09">2$\nwarrow$</font> | <font color="#e36c09">2$\leftarrow$</font> | 2                                          | 2                                         |
| 4   | B     | 0                              | 1$\nwarrow$                              | 1                                          | 2$\uparrow$                              | 2$\uparrow$                                | <font color="#e36c09">3$\nwarrow$</font>   | 3$\leftarrow$                             |
| 5   | D     | 0                              | 1$\uparrow$                              | 2$\nwarrow$                                | 2                                        | 2                                          | <font color="#e36c09">3$\uparrow$  </font> | 3                                         |
| 6   | A     | 0                              | 1$\uparrow$                              | 2$\uparrow$                                | 2                                        | 3$\nwarrow$                                | 3                                          | <font color="#e36c09">4$\nwarrow$</font>  |
| 7   | B     | 0                              | 1$\nwarrow$                              | 2$\uparrow$                                | 2                                        | 3$\uparrow$                                | 4$\nwarrow$                                | <font color="#e36c09">4$\uparrow$ </font> | 
- value different (from $\leftarrow$  or $\uparrow$  max value) / (no arrow means $\leftarrow\uparrow$ same value)
- value same (from $\nwarrow$ value + 1)
```pseudo
LCS-LENGTH(X,Y)
1	m = X.length
2	n = Y.length
3	let b[1..m][1..n] and c[0..m][0..n] be new tables
4	for i = 1 to m
5		c[i][0] = 0
6	for i = 1 to m
7		for j = 1 to n
8			if X[i] == Y[i]
9				c[i][j] = c[i-1][j-1] + 1
10				b[i][j] = "↖"
11			elsif c[i-1][j] ≥ c[i][j-1]
12				c[i][j] = c[i-1][j]
13				b[i][j] = "↑"
14			else c[i][j] = c[i][j-1]
15				b[i][j] = "←"
16	return c and b

PRINT-LCS(b,X,i,j)
1	if i == 0 or  j == 0
2		return
3	if b[i][j] == "↖"
4		PRINT-LCS(b,X,i-1,j-1)
5		print X[i] or Y[j]
6	elseif b[i][j] == "↑"
7		PRINT-LCS(b,X,i-1,j)
8	else PRINT-LCS(b,X,i,j-1)
```

### Performance
- Space consumption
	- Table c : mn
	- Table b : mn
	- $\Theta(mn)$ elements in total                                                                                                   
- Running time
	- $\Theta(1)$ for an entry
	- $\Theta(mn)$ time in total

- Space reduction : $\Theta(min(m,n))$ (LCS length only)


