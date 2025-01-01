```c
#include <stdlib.h>
void *malloc(size_t size)
void free(void *p)
```
## $\text{void *malloc(size\_t size)}$
- Successful 
	- Returns a pointer to a memory block of at least **size** bytes aligned to an 8-byte (x86) or 16-byte (x86-64) boundary
	- If **size == 0**, returns NULL
- Unsuccessful 
	- Returns NULL(0) and sets **errno**
## $\text{void free(void *p)}$
- Returns the block pointed at by **p** to pool of available memory
- **p** must come from a previous call to **malloc** or **realloc**
## Other functions
- $\text{calloc}$ : Version of $\text{malloc}$ that initializes allocated block to zero
- $\text{realloc}$ : Changes the size of a previously allocated block
- $\text{sbrk}$ : Used internally by allocators to grow or shrink the heap
## Allocation Example
- ![](https://i.imgur.com/6cZmibo.png)
	- !caution : square means that word(int) size
## Constraints
- Applications
	- Can issue arbitrary sequence of malloc and free requests
	- free request must be to a malloc’d block
- Allocators
	- Can’t control number or size of allocated blocks
	- Must respond immediately to malloc requests
		- i.e., can’t reorder or buffer requests
	- Must allocate blocks from free memory
		- i.e., can only place allocated blocks in free memory
	- Must align blocks so they satisfy all **alignment requirements** 8-byte (x86) or 16-byte (x86-64) alignment on Linux boxes
	- Can manipulate and modify only free memory
	- Can’t move the allocated blocks once they are malloc’d
		- i.e., compaction is not allowed
## Performance
- Goals : maximize throughput and peak memory utilization (these goals are often conflicting)
	- Performance Goal 1 : Throughput
		- Throughput
			- Number of completed requests per unit time
	- Performance Goal 2 : Peak Memory Utilization
		- Definition : Aggregate payload $P_k$
			- **malloc(p)** results in a block with a payload of **p** bytes
			- After request $R_k$ has completed, the aggregate payload $P_k$ is the sum of currently allocated payloads
		- Definition : Current heap size $H_k$
			- Assume $H_k$ is monotonically non-decreasing
				- i.e., heap only grows when allocator uses **sbrk**
		- Definition : Peak memory utilization after k+1 requests
			- $U_k=(max_{i\leq k}\ P_i) / H_k$
## Fragmentation
- Poor memory utilization caused by <font color="#fac08f">fragmentation</font>
- Internal fragmentation
	- ![](https://i.imgur.com/1Xp3SaM.png)
	- For a given block, internal fragmentation occurs if payload is smaller than block size
	- Caused by
		- Overhead of maintaining heap **data structures**
		- **padding** for alignment purposes
		- Other explicit policy decisions
			- (e.g., to return a big block to satisfy a small request)
		- Depends only on the pattern of previous requests
			- Thus, easy to measure
- External fragmentation
	- ![](https://i.imgur.com/Mpq9Td9.png)
	- Occurs when there is enough aggregate heap memory, but no single free block is large enough
	- Depends on the pattern of future requests
		- Thus, difficult to measure
## Implementation Issues
- Q1. How do we know how much memory to free given just a pointer?
	- $\text{free(p)}$ ...?
- Q2. How do we keep track of the free blocks? 
- Q3. What do we do with the extra space when allocating a structure that is smaller than the free block it is placed in?
- Q4. How do we pick a block to use for allocation -- many might fit?
- Q5. How do we reinsert freed block?
	- 2 ~ 5 : $\text{malloc}$ ...? (which datastructure : **free (block) list**)
## Knowing How Much to Free
- Standard method
	- Keep the length of a block in the word preceding the block
		- This word is often called the <font color="#fac08f">header field</font> or <font color="#fac08f">header</font>
	- Requires an extra word for every allocated block
	- ![](https://i.imgur.com/fhuoW48.png)
- [[Implicit Free List]] : using length - links all blocks
- Explicit list - among the free blocks using pointers
	- Maintain list(s) of free blocks, not all blocks
		- The  "next" free block could be anyware
			- So we need to store forward/back pointers, not just sizes 
		- Still need boundary tags for coalescing
		- Luckily we track only free blocks, so we can use payload area
		- ![](https://i.imgur.com/kS3l5OC.png)
- Segregated free list - different free lists for different size classes
	- Each <font color="#fac08f">size class</font> of blocks has its own free list
		- ![](https://i.imgur.com/eaTExim.png)
	- Often have separate classes for each small size
	- For larger sizes : One class for each two-power size
- Blocks sorted by size - can use a balanced tree with pointers within each free block, and the length used as a key