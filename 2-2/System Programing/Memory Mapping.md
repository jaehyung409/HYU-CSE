## Memory Mapping
- VM areas initialized by associating them with disk objects
	- Process is known as <font color="#fac08f">memory mapping</font>
- Area can be *backed* by (i.e., get its initial values from)
	- <font color="#fac08f">Regular file</font> on disk (e.g., an executable object file)
		- Initial page bytes come from a section of a file
		- Zero-padded if the area is larger than the section of the file
	- <font color="#fac08f">Anonymous file</font> (e.g., nothing)
		- First [[Faults#EX Page Fault|faults]] lt will allocate a physical page full of 0's (<font color="#fac08f">demand-zero page</font>)
		- Once the page is written to (<font color="#fac08f">dirtied</font>), it is like any other page
- Dirty pages are copied back and forth between memory and a special <font color="#fac08f">swap file</font>
## Shared Objects
- ![](https://i.imgur.com/keTMtr7.png)
- Private COW Objects
	- Processes mapping a private <font color="#fac08f">copy-on-write(COW)</font> object
		- Not logically shared, but physically shared
			- ![](https://i.imgur.com/0ddO0pX.png)
		- Instruction writing to private page triggers protection fault
			- ![](https://i.imgur.com/EP6XPnP.png)
- The $\text{fork()}$ Revisited
	- VM and memory mapping explain how $\text{fork}$ provides private address space for each process
	- To create virtual address for new process
		- Create exact copies of current $\text{mm\_struct, vm\_area\_struct}$ and page tables 
		- Flag each page in both processes as read-only
			- write -> fault (anonymous file -> COW )
		- Flag each $\text{vm\_area\_struct}$ in both processes as private COW
	- On return, each process has exact copy of virtual memory
	- Subsequent writes create new pages using COW mechanism
- The $\text{execve()}$ Revisited
	- ![](https://i.imgur.com/OJwOnDM.png)
## User-Level Memory Mapping
```c
void *mmap(void *start, int len, int prot, int flags, int fd, int offset);
```
- Map $\text{len}$ bytes starting at offset $\text{offset}$ of the file specified by file description $\text{fd}$, preferably at address $\text{start}$
	- $\text{start}$ : may be 0 for "pick an address"
	- $\text{prot}$ : PROT_READ, PROT_WRITE, ...
	- $\text{flags}$ : MAP_ANON, MAP_PRIVATE, MAP_SHARED, ...
- Return a pointer to start of mapped area (may not be $\text{start}$)
- ![](https://i.imgur.com/BGsFtlR.png)
- Cat
	- ![](https://i.imgur.com/xVCU1u6.png)
