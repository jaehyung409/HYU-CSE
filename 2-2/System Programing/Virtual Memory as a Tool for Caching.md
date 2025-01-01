## Virtual Memory as a Tool for Caching
- Conceptually, <font color="#fac08f">virtual memory</font> is an array of N contiguous bytes stored on disk
- The contents of the array on disk are cached in <font color="#fac08f">physical memory</font> (or <font color="#fac08f">DRAM cache</font>)
	- These cache blocks are called **pages**, whose size is $P=2^p$ bytes![](https://i.imgur.com/X9E7Nu8.png)
## DRAM Cache Organization
- DRAM cache organization driven by the huge <font color="#fac08f">miss penalty</font>
	- DRAM is about <font color="#fac08f">10x</font> slower than SRAM (cache memory)
	- Disk is about <font color="#fac08f">10000x</font> slower than DRAM (main memory)
	- Virtual memory seems terribly inefficient, but it works well
	- [[Locality]] greatly helps virtual memory
	- At any point in time, programs tend to access a set of active virtual pages called the <font color="#fac08f">working set</font>
		- Programs with better temporal locality will have smaller working sets
		- working set size < main memory size
			- Good performance for one process after compulsory misses
		- SUM(working set sizes) > main memory size
			- ***Thrashing*** : Performance meltdown where pages are swapped (copied) in and out conntinuously
- Consequences
	- Large page (block) size : typically 4 KB (sometimes 4 MB)
	- Fully associative
		- Any VP can be placed in any PP
		- Requires a "large" mapping function
			- different from cache memories
	- Highly sophisticated, expensive replacement algorithms
		- Too complicated and oped-ended to be implemented in hardware
	- Write-back rather than Write-through
## Core Data Structure in Virtual Memory
![](https://i.imgur.com/L0NPiYe.png)
- A <font color="#fac08f">page table</font> is an array of page table entries(PTEs) that maps virtual pages to physical pages
	- Per-process kernel data structure in DRAM
## Page Hit
- Page hit : reference to VM word that is in physical memory (DRAM cache hit)
- ![](https://i.imgur.com/PzKYVne.png)
## Page Fault
- Page fault : reference to VM word that is not in physical memory (DRAM cache miss)
- ![](https://i.imgur.com/aN9gqyI.png)
### Handling Page Fault
1. Page miss causes page fault (an exception)
2. Page fault handler selects a <font color="#fac08f">victim</font> to be evicted (swap)
3. Offending instruction is restarted $\rightarrow$ Now page hit!
- Key point : Waiting until the miss to copy the page to DRAM is known as <font color="#fac08f">demand paging</font>
## Allocating Pages
- Allocating a new page of virtual memory![](https://i.imgur.com/OsyWUr1.png)
