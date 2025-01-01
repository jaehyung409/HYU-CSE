#datastructure 
# Array Allocation
- ### Basic Principle
    >T A\[L]
	- Array of data <font color="#de7802">type T</font> and <font color="#de7802">length L</font>
	- Contiguously allocated region of *L* \* **sizeof**(T) bytes in memory
	- Identifier **A** can be used as a pointer to array element 0 : Type $T^*$
	- In two or more arrays, Not guaranteed to allocate successive
- ### Array Accessing
``` assembly
movl (%rdi, %rsi, 4) //z[digit]
```

- ### Multidimensional (Nested) Arrays
    >T A\[R]\[C]
	- 2D array of <font color="#de7802">data type T</font>
	- R rows, C columns
	- Type *T* element requires *K* bytes
	- Array Size : R \* C \* K bytes
	- Arrangement (<font color="#92cddc">Row-Majot Ordering</font>)

|                     int A\[R]\[C](4 \* R \* C bytes)                      | <                                                      | <   | <                                                          |
|:------------------------------------------------------:| ------------------------------------------------------ | --- | ---------------------------------------------------------- |
| <font color="#de7802">A\[0]\[0] ... A\[0]\[C-1]</font> | <font color="#ffc000">A\[1]\[0] ... A\[1]\[C-1]</font> | ... | <font color="#76923c">A\[R-1]\[0] ... A\[R-1]\[C-1]</font> |
- Row Vectors
	- **A\[i]** is array of C elements
	- Each element of type *T* requires *K* bytes
	- Address $A+i*(C*K)$
- Nested Array Element Access
	- Address $A+(i*C+j)*K$
```c
int get_pgh_digit (int index, int dig){
	return pgh[index][dig]
}
```
```assembly
leaq (%rdi, %rdi, 4), %rax # 5 * index
addl %rax, % rsi           # 5 * index + dig
movl pgh(, %rsi, 4), % eax # M[pgh + 4 * (5 * index + dig)]
```
- Multi-Level Array
	- Array of Array
	- Must do two memory reads
		- First get pointer to row array
		- Then acess element within array
		- Mem\[Mem\[univ + 8\*index] + 4\*digit]
```c
int get_univ_digit (size_t index, size_t digit){
	return univ[index][dig]
}
```
```assembly
salq $2, %rsi             # 4 \* digit
addq univ(,%rdi,8), %rsi  # p = univ[index] + 4 * digit
movl (%rsi), %eax         # return *p
```
- Nested Array vs Multi-Level Array
	- Fast vs Slow (\# of Memory Accessing, Nested Array is good(only once))
	- Memory efficiency (Multi-Level Array is good)
- N X N Matrix Code
```c
#define N 16
typedef int fix_matrix[N][N];
/* Get element a[i][j] */
int fix_ele(fix matrix a, size_t i, size_t j){ return a[i][j]; }

/* traditional way to implement dynamic arrays */
#define IDX(n, i ,j) ((i) * (n) + (j))
/* Get element a[i][j] */
int vec_ele(size_t n, int *a, size_t i, size_t j){ return a[IDX(n, i, j)]; }

/* Variable dimensions, implicit indexing, now supported gcc*/
int var_ele(size_t n, int a[n][n], size_t i, size_t j){ return a[i][j]; }
```