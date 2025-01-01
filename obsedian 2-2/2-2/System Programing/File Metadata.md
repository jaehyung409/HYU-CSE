## File Metadata
- File contents are data
	- A Linux file is a sequence of m bytes
		- $B_0, B_1,\cdots,B_{m-1}$
		- Each process manages its own file cursor
- Metadata is data about data
	> Processes manages the same metadata about the same file
	- File acacess : read/write/execution permission
	- File size
	- File type
- ![](https://i.imgur.com/yhXynD7.png)
	- <font color="#fac08f">Per-process</font> metadata maintained by kernel
		- Different processes manage different file cursors
		- A processes manages different cursors in the same file
	- <font color="#fac08f">Per-file</font> metadata maintained by kernel
		- accessed by users with the **stat** and **fstat** functions
### Example of Accessing File Metadata
- ![](https://i.imgur.com/E435uDJ.png)
