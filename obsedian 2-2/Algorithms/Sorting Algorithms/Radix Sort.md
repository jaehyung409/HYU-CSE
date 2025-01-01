#algorithms #sorting 

reference : 
- [Radix Sort - 데이터 구조 및 알고리즘 튜토리얼 - GeeksforGeeks](https://www.geeksforgeeks.org/radix-sort/?ref=gcse_ind)
- Introductions to algorithms, 3rd


![](https://media.geeksforgeeks.org/wp-content/uploads/20230609164536/Radix-Sort--1.png)

- Description : A Linear-time Sorting Alogrithm that sorts elements by processing them digit by digit 
- Repeatedly Sorting
	- based  on each digit's value
	- LSD -> MSD, MSD -> LSD
- Using Counting Sort as a subroutine to sort.

### Code
```pseudo code
RADIX-SORT(A,d)
	for i = 1 to d
		use a stable sort to sort array A on digit i
```

### Performance : 
- Radix Sort sorts in $\Theta(d(n + k))$ when n d-digit numbers are given and each digit can take on up to k possible values
	- Changing d and k.
		- Given b-bit numbers.
		- d : b /r ; r-bit is number of bits to compare at a time
		- k : r-bit's range ($base^{r}$, In binary, $2^r$)
	- Given n b-bit numbers and any positive integer r $\leq$ b, RADIX-SORT correctly sorts these numbers in $\Theta((b/r)(n+2^r))$ time.
		- Computing optimal $r$ minimizing $(b/r)(n+2^r)$
			1. $b < \lfloor\lg n\rfloor$ : $r= b$
			2. $b \geq \lfloor\lg n\rfloor$ : $r = \lfloor \lg n \rfloor$
- when d is constant and  $k =O(n)$, Radix Sort runs in linear time.


### Vs. Quick Sort
$$\begin{align} if\  b=\Theta(\lg n), we\ choose\ r \approx \lg n 
\\ Radix\ Sort &: \Theta(n)
\\ Quick\ Sort &: \Theta(n\lg n) &&&&&&&&&&&&&&&&&&&&&&&&\end{align}$$
hidden in th $\Theta$-notation differ.
1. Radix Sort may make fewer passes than quicksort over the n keys, each pass of radix sort may take significantly longer.
2. Radix Sort does not sort in place