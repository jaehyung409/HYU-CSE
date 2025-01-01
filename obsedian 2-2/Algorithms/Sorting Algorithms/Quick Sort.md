#algorithms #sorting

reference : 
-  [빠른 정렬 - GeeksforGeeks](https://www.geeksforgeeks.org/quick-sort-algorithm/?ref=header_outind)
-  Introductions to algorithms, 3rd


![](https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/01/QuickSort2.png)

- Desription : A sorting algorithms using partition (pivot)
- Pivot 
	- Purpose : To create balanced partitions
	- How : 
		1. first / last element
		2. random element
		3. median-of-Three : get_mid(first, last, middle)
- Partition
	1. Partition the array around pivot
	2. left element < pivot & pivot < right elemnet
- A divide-and-conquer paradigm
	- Divide : Select pivot, and partition
	- Conquer : Recursively call for two partitioned subarrays (~ only one element is left)

### Code
```pseudo
QUICKSORT(A,p,r)
1	if p < r
2		q = PARTITION(A,p,r)
3		QUICKSORT(A,p,q - 1)
4		QUICKSORT(A,q + 1,r)

PARTITION(A,p,r)
1	x = A[r]
2	i = p - 1
3	for j = p to r - 1
4		if A[j] <= x
5			i = i + 1
6			exchange A[i] with A[j]
7	exchange A[i+1] with A[r]
8	return i + 1
```


### Performance :
- Partition : $\Theta(n)$
- Balanced partitioning (Best Case) : $\Theta(n\lg n)$
- Unbalanced partitioning (Worst Case) : $\Theta(n^2)$
- Average Case : $\Theta(n\lg n)$
$$\begin{align*} E[T(n)]&=a 
\end{align*}$$
