#algorithms #sorting 

reference : 
- [카운팅 정렬 - 데이터 구조 및 알고리즘 튜토리얼 - GeeksforGeeks](https://www.geeksforgeeks.org/counting-sort/?ref=header_outind)
- Introductions to algorithms, 3rd


![](https://media.geeksforgeeks.org/wp-content/uploads/20230920182656/5.png)

- Description : A Linear-time Sorting Alogrithm
- I

### Code
```pseudo code
COUNTING-SORT(A,B,k)
1	for i = 0 to k
2		C[i] = 0
3	for j = 1 to A.length
4		C[A[j]] = C[A[j]] - 1
5	> C[i] contains the number of elements equal to i.
6	for i = 1 to k
7		C[i] = C[i] + C[i - 1]
8	> C[i] contains the number of elements less than or equal to i.
9	for j = A.length downto 1
10		B[C[A[j]]] = A[j]
11		C[A[j]] = C[A[j]] - 1
```

### Performance : 
- The overall time is $\Theta(k + n)$ where $k$ is the range of input integers.
- If $k =O(n)$, the running time is $\Theta(n)$