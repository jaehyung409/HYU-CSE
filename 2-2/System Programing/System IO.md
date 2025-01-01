#io 
## Unix I/O
- ### Overview
	- I/O is the process of copying data between main memory and external devices
	- A Linux *<font color="#fac08f">file</font>* is a sequence of **m** bytes
		- $B_0, B_1,\cdots B_{m-1}$
	- Elegant mapping of files to devices allow kernal to export **simple interface** called <font color="#d99694">Unix I/O</font>
		- $\text{open()}$ and $\text{close()}$
		- $\text{read()}$ and $\text{write()}$
		- Changing the <font color="#d99694">current file position</font> (seek) indicates next offset into file to read or write 
			- $\text{lseek()}$
## Pros and Cons of Unix I/O
- Pros
	- Unix I/O is the most general and lowest overhead form of I/O
	- All other I/O packages are implemented using Unix I/O functions
	- Unix I/O provides functions for accessing file metadata
	- Unix I/O functions are async-signal-safe and can be used safely in signal handlers
- Cons
	- Dealing with short counts is tricky and error prone
	- Efficient reading of text lines requires some form of buffering, also tricky and error prone
	- Both of these issues are addressed by the standard I/O and RIO packages
## Simple Unix I/O example (echo)
- Copying **stdin** to **stdout**, one byte at a time , ref : [[CSapp_h]]
```c
#include "csapp.h"

int main(void){
	char c;
	
	while(Read(STDIN_FILENO, &c, 1) != 0)
		Write(STDOUT_FILENO, &c, 1);
	exit(0);
}
```

## File Types![[File Types]]
## Files![[Files]]
