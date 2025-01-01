## Implicit Lists
- using length - links all blocks
- For each block we need both size and allocation status
	- Could store this information in two words : wasteful !
- Standard trick
	- If blocks are aligned, some low-order address bits are always 0
	- Instead of storing an always-0 bit, use it as a allocated/free flag
	- When reading size word, must mask out this bit
	- ![](https://i.imgur.com/yTLIejB.png)
- ![](https://i.imgur.com/b1D1Xum.png)
## Finding a Free Block
- First fit
	- Search list from beginning, choose first free block that fits
	- Can take linear time in total number of blocks (allocated and free)
	- In practice it can cause "splinters" at beginning of list
```c
p = start;
while ((p < end) &&    // not passed end
	   ((*p & 1) ||    // already allocated
	   (*p <= len)))   // too small
	p = p + (*p & -2); // goto next block (word addressed)
```
- Next fit
	- Like first fit, but search list starting where previous search finished
	- Should often be faster than first fit 
		- avoids re-scanning unhelpful blocks
	- Some research suggests that fragmentation is worse
- Best fit
	- Search the list, choose the **best** free block
		- fits, with fewest bytes left over
	- Keeps fragments small
		- usually improves memory utilization
	- Will typically run slower than first fit
## Allocating in Free Block : Splitting
- Since allocated space might be smaller than free space, we might want to split the block
- ![](https://i.imgur.com/ldYoJwa.png)
```c
void addblock(ptr p, int len){
	int newsize = ((len + 1) >> 1) << 1;   // round up to even
	int oldsize = *p & -2;                 // mask out low bit
	*p = newsize | 1;                      // set new length
	if (newsize < oldsize)
		*(p + newsize) = oldsize - newsize // set length in remaining
}                                          //  part of block
```
- Freeing a Block
	- Simplest implementation
		- Need only clear the "allocated" flag
			- `void free_block(ptr p) { *p = *p & -2; }`
		- But can lead to "false fragmentation"
			- ![](https://i.imgur.com/nQzoJLD.png)
			- There is enough free space, but the allocator won't be able to find it
## Coalescing
- Join (coalesce) with next/previous blocks, if they are free
	- Coalescing with next block
	- ![](https://i.imgur.com/ULyI8Kq.png)
```c
void free_block(ptr p){
	*p = *p & -2;
	next = p + *p;
	if ((*next & 1) == 0)
		*p = *p + *next;
}
```
- Bidirectional Coalescing
	- Boundary tags \[Knuth73]
		- Replicate size/allocated word at "bottom" (end) of free blocks
		- Allows us to traverse the "list" backwards, but requires extra space
		- Important and general technique
		- ![](https://i.imgur.com/CdBVW1k.png)
	- Constant Time Coalescing
		- ![|400](https://i.imgur.com/ny2Nj9s.png)
	- Disadvantage of Boundary Tags
		- Internal fragmentation
			- Space required for header and footer
				- Only free blocks use footer tag!
- Optimized Coalescing
	- free blocks use footer tag
	- xxx0x : previous "free"
	- xxx1x : previous "set"
	- ![|400](https://i.imgur.com/DuqOjL2.png)
## Complexity
- Throughput
	- Allocate cost : linear time worst case
	- Free cost : constant time worst case even with coalescing
- Memory usage
	- Depends on placement poilcy
		- First-fit, next-fit or best-fit
- Too simple to be used in practice
	- However, the concepts of splitting and boundary tag coalescing are general to all allocators
