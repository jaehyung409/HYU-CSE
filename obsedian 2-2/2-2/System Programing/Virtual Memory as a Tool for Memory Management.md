## Virtual Memory as a Tool for Memory Management
- ![](https://i.imgur.com/Z4DOkcA.png)
- Key idea : each process has its own virtual address space
	- It can view memory as a simple linear array
	- Mapping function scatters addresses through physical memory
		- Well-chosen mappings can improve [[Locality]]
- Simplifying memory allocation
	- Each virtual page can be mapped to any physical page
	- A virtual page can be stored in different physical pages at different times
- Sharing code and data among processes
	- Map virtual pages to the same physical page
## Simplifying Linking and Loading
- Linking
	- Each program has similar virtual address space
	- Code, data, and heap always start at the same addresses
- Loading 
	- **execve** allocates virtual pages for $\text{.text}$ and $\text{.data}$ sections & creates PTEs(page table entries) marked as invalid
	- The $\text{.text}$ and $\text{.data}$ sections are copied, page by page, on demand by the virtual memory system
- ![|400](https://i.imgur.com/fllttkx.png)