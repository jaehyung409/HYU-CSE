#dp #algorithms
reference : 
- [Rod Cutting - GeeksforGeeks](https://www.geeksforgeeks.org/cutting-a-rod-dp-13/?ref=header_outind)
- Introductions to algorithms, 3rd

### Problems
> Given a rod of length $n$ inches and a table of prices $p_i$ for $i = 1,2,...n$, determine the maximum revenue $r_n$ obtainable by cutting up the rod and selling the pices

| length $i$ | 1     | 2     | 3     | ... | n     |
| ---------- | ----- | ----- | ----- | --- | ----- |
| price $i$  | $p_1$ | $p_2$ | $p_3$ | ... | $p_n$ |

### Dynamic Programing
- $r_n = max_{1\leq i \leq n}(p_i+r_{n-i})$
- $s_n = i\ (when\ \ r_n = max)$
```pseudo
EXTENDED-BOTTOM-UP-CUT-ROD(p,n)
1	let r[0 .. n] and s[0 .. n] be new arrays
2	r[0] = 0
3	for j = 1 to n
4		r[j] = -∞
5		for i = 1 to j
6			if r[j] < p[i] + r[j-i]
7				r[j] = p[i] + r[j-i]
8				s[j] = i
9	return r and s

PRINT-CUT-ROD-SOLUTION(p,n)
	(r,s) = EXTENDED-BOTTOM-UP-CUT-ROD(p,n)
	while n > 0
		print s[n]
		n = n - s[n]
```

### Performance
- Space consumption
	- Table r : n
	- Table s : n
	- $\Theta(n)$ elements in total                                                                                                   
- Running time
	- $1 + 2 + ... + n = n(n+1)/2$
	- $\Theta(n^2)$ time in total

- Table $r$ can be reduced like table $s$ in [[Assembly-line Scheduling#^0bd1f9|Assembly-line Scheduling]]?
	- No. It needs all previous results.


