# Cache & Virtual Memory
1. [[Address Spaces]]
2. [[Cache|General cache concepts]]
3. [[Virtual Memory as a Tool for Caching]]
4. [[Virtual Memory as a Tool for Memory Management]]
5. [[Virtual Memory as a Tool for Memory Protection]]
6. [[Memory Mapping]]
7. Summary
	- Programmer's view of virtual memory
		- Each process has its own private linear address space
		- Can't ve corrupted by other processes
	- System view of virtual memory
		- Uses memory efficiently by caching virtual memory pages
			- Efficient only because of locality
		- Simplifies memory management and programming
		- Simplifies protection by providing a convenient interpositioning point to check permissions