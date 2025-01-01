#algorithms #sorting

reference : 
- [삽입 정렬 알고리즘 - GeeksforGeeks](https://www.geeksforgeeks.org/insertion-sort-algorithm/?ref=gcse_ind)
- Introductions to algorithms, 3rd


![](https://media.geeksforgeeks.org/wp-content/uploads/20240802210251/Insertion-sorting.png)

- Description : A Sorting Alogrithm using Insertion
- Insertion -> A key  to(insert) a sorted list of keys (preserving the sorted order)
### Code
```pseudo code
INSERTION-SORT(A)                            
1	for j = 2 to A.length                    
2		key = A[j]                           
3		// Insert A[J] into the sorted sequence A[1..j - 1]
4		i = j - 1                            
5		while i > 0 and A[i] > key            
6			A[i + 1] = A[i]                  
7			i = i - 1               
8		A[i + 1] = key                      
```

### Performance : 
$$T(n) = c_1n+c_2(n-1)+c_4(n-1)+c_5\sum_{j=2}^nt_j+c_6\sum_{j=2}^n(t_j-1)+c_7\sum_{j=2}^n(t_j-1)+c_8(n-1)$$
- best case : $\Omega(n), \  t_j = 1$, pre-sorted array
- worst case : $\Theta(n^2),\ t_j = j$, inverse-sorted array (Decreasing Array)
- general case : $O(n^2)$

| **Insertion-Sort(A)** | **cost** | **times**             |
| --------------------- | -------- | --------------------- |
| **line 1**                | $c_1$    | n                     |
| **line 2**                | $c_2$    | $n-1$                 |
| **line 3**                | 0        | $n-1$                 |
| **line 4**                | $c_4$    | $n - 1$               |
| **line 5**                | $c_5$    | $\sum_{j=2}^nt_j$     |
| **line 6**                | $c_6$    | $\sum_{j=2}^n(t_j-1)$ |
| **line 7**                | $c_7$    | $\sum_{j=2}^n(t_j-1)$ |
| **line 8**                | $c_8$    | $n-1$                 |
