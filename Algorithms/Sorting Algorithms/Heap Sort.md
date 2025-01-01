#algorithms #sorting #heaps

reference : 
- [힙 정렬 - 데이터 구조 및 알고리즘 튜토리얼 - GeeksforGeeks](https://www.geeksforgeeks.org/heap-sort/?ref=shm#heap-sort-algorithm)
- [[Heap]] 
- Introductions to algorithms, 3rd


![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/binaryheap.png)

- Description : A Sorting Alogrithm using Heaps
- Heaps ![[Heap#Heap Structure]]
- Like merge sort (Running time), insertion sort (in place)
### Code
```pseudo code
BUILD-MAX-HEAP(A)
1	A.heap-size = A.length
2	for i = ⌊A.length / 2⌋ downto 1
3		MAX-HEAPIFY(A,i)

MAX-HEAPIFY(A,i)
1	l = Left(i)
2	r = Right(i)
3	if l ≤ A.heap-size and A[l] > A[i]
4		largest = l
5	else largest = i
6	if r ≤ A.heap-size and A[r] > A[largest]
7		largest = r
8	if largest ≠ i
9		exchange A[i] with A[largest]
10		MAX-HEAPIFY(A,largest)

HEAPSORT(A)
1	BUILD-MAX-HEAP(A)
2	for i = A.length down to 2
3		exchange A[1] with A[i]
4		A.heap-size = A.heap-size - 1
5		MAX-HEAPIFY(A,1)
```

### Performance : 
- Building a heap : $O(n)$
	- Upper bound : $O(n\lg n)$
		- MAX-HEAPIFY costs $O(\lg n)$, call $O(n)$
	- Tight bound : $O(n)$
		- MAX-HEAPIFY to run at a node varies with the height of the node in the tree.
		- Our tighter analysis relies on the properties that an n-element heap has height $\lfloor \lg n\rfloor$ and at most $\lceil n/2^{h+1}\rceil$ nodes of any height $h$.
		- running time of MAX-HEAPIFY on a node of height $h$ is $O(h)$, 
		  So total cost of BUILD-MAX-HEAP : $$\sum_{h=0}^{\lfloor \lg n \rfloor}{\lceil\frac{n}{2^{h+1}}\rceil}O(h) = O(n\sum_{h=0}^{\lfloor \lg n\rfloor}{\frac{h}{2^h}}) < O(n\sum_{h=0}^\infty{\frac{h}{2^h}}) = O(n)$$
- Extract max $O(\lg n)$ for n times : $O(n\lg n)$
- Heap Sort : $O(n\lg n )$
