#algorithms #sorting

reference : 
-  [병합 정렬 - 데이터 구조 및 알고리즘 튜토리얼 - GeeksforGeeks](https://www.geeksforgeeks.org/merge-sort/?ref=header_outind)
-  Introductions to algorithms, 3rd


![](https://media.geeksforgeeks.org/wp-content/uploads/20230706153706/Merge-Sort-Algorithm-(1).png)

- Desription : A sorting algorithms using merge
- Merge : Given two sorted lists of keys -> generate a sorted list
- A divide-and-conquer approach
	- Divide : Divide the n keys into two lists of n/2 keys
	- Conquer : Sort the two lists recursively using merge sort
	- Combine : Merge the two sorted lists

### Code
```pseudo
MERGE-SORT(A,p,r)
1	if p<r
2		q = ⌊(p + r) / 2⌋
3		MERGE-SORT(A,p,q)
4		MERGE-SORT(A,q + 1, r)
5		MERGE(A,p,q,r)
		
MERGE(A,p,q,r)
1	n1 = q - p + 1
2	n2 = r - q
3	let L[1 .. n1 + 1] and R[1 .. n2 + 1] be new arrays
4	for i = 1 to n1
5		L[i] = A[p + i - 1]
6	for j = 1 to n2
7		R[j] = A[q + j]
8	L[n1 + 1] = infinite
9	R[n2 + 1] = infinite
10	i = 1
11	j = 1
12	for k = p to r
13		if L[i] <= R[j]
14			A[k] = L[i]
15			i = i + 1
16		else 
17			A[k] = R[j]
18			j = j + 1
```


### Performance :
$$
T(n) = \begin{cases}\Theta(1) \qquad \quad \qquad \qquad if \ n = 1, \\ 2T(n/2) +\Theta(n) \qquad if \: n > 1 \end{cases}
$$
- Always : $\Theta(n\log{n})$

| **Step**          | **Running time** | **explanation**                                          |
| :---------------- | :--------------- | :------------------------------------------------------- |
| **Divide(2)**     | $\Theta(1)$      | The divide step just computes the middle of subarray     |
| **Conquer(3, 4)** | 2T(n / 2)        | We recursively solve two subproblems, each of size n / 2 |
| **Combine(5)**    | $\Theta(n)$      |                                                          |
Combine (Merge) Running time
- let n1 and n2 denote the length of two sorted lists.
- $\Theta(n_1+n_2)$ time
	- Main operations : compare(13, 16) and move(4 ~ 7, 14, 17)
	- number of ; $\#comparison \leq \#movement$
	- Obviously, $\#movement = n_1 + n_2$ 
	- So, $\#comparison \leq n_1 + n_2$