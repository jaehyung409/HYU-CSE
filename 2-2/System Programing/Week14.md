# Dynamic Memory Allocation : Basic Concepts
1. [[Dynamic Memory Allocation|Basic concepts]]
2. [[Implicit Free List]]
3. Summary of Key Allocator Policies
	- Placement policy
		- First-fit, next-fit, best-fit, etc.
		- Trades off lower throughput for less fragmentation
		- **Interesting observation** : segregated free lists approximate a best fit placement policy without having to search entire free list
	- Splitting policy:
		- When do we go ahead and split free blocks?
		- How much internal fragmentation are we willing to tolerate?
	- Coalescing policy:
		- **Immediate coalescing** : coalesce each time free is called 
		- **Deferred coalescing** : try to improve performance of free by deferring coalescing until needed 
			- Examples
				- Coalesce as you scan the free list for malloc
				- Coalesce when the amount of external fragmentation reaches some threshold