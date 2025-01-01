#dp #algorithms 
reference : 
- [Assembly Line Scheduling | DP-34 - GeeksforGeeks](https://www.geeksforgeeks.org/assembly-line-scheduling-dp-34/?ref=header_outind)
- Introductions to algorithms, 3rd

### Problems
![](https://media.geeksforgeeks.org/wp-content/uploads/AssembleScheduling1.png)
- $n$ stations : $S_i$
- Assembly time in the $i$th station $a_i$
- entry time : $e$
- Exit time : $x$

### Brute-Force approaching
- Enumerate all possible ways and find a fastest way.
- There are $2^n$ possible ways : Too Many

### Dynamic Programing
- The faster way to $S_{i,j}$ goes through $S_{1,j-1}$ or $S_{2,j-1}$
```pseudo
FASTEST-WAY(a,t,e,x,n)
1	s[1][1] = e[1]+a[1][1]
2	s[2][1] = e[2]+a[2][1]

3	for j = 2 to n
4		if s[1][j-1] ≤ s[2][j-1] + t[2][j-1]
5			s[1][j] = s[1][j-1] + a[1][j]
6			l[1][j] = 1
7		else s[1][j] = s[2][j-1] + t[2][j-1] + a[1][j]
8			l[1][j] = 2

9		if s[2][j-1] ≤ s[1][j-1] + t[1][j-1]
10			s[2][j] = s[2][j-1] + a[2][j]
11			l[2][j] = 2
12		else s[2][j] = s[1][j-1] + t[1][j-1] + a[2][j]
13			l[2][j] = 1

14	if s[1][n] + x[1] ≤ s[2][n] + x[2]
15		s* = s[1][n] + x[1]
16		l* = 1
17	else s* = s[2][n] + x[2]
18		l* = 2

PRINT-STATIONS(l,l*,n)
1	i = l*
2	print "line "i", station "n"
3	for j = n down to 2
4		i = l[i][j]
5		print "line "i", station "j-1"
```

### Performance
- Space consumption
	- Table S : 2n
	- Table l : 2n
	- $\Theta(n)$ elements in total                                                                                                   
- Running time
	- Computing each element requests $\Theta(1)$ time.
	- $\Theta(n)$ time in total

- Fastest time only ^0bd1f9
	- $\Theta(1)$ space
		- Table l is not necessary
		- Table S
			- 2n elements -> 4 elements



