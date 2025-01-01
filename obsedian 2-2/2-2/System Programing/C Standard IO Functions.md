## Standard I/O Functions
- The C standard library ($\text{libc.so}$) contains a collection of higher-level <font color="#fac08f">standard I/O</font> functions
- ##### Examples of standard I/O functions
	- Opening and closing files (**fopen** and **fclose**)
	- Reading and writing bytes (**fread** and **fwrite**)
	- Reading and writing text lines (**fgets** and **fputs**)
	- Formatted reading and writing (**fscanf** and **fprintf**)
## Standard I/O Streams
- Standard I/O models open files as <font color="#fac08f">streams</font>
	- Abstraction for a file descriptor and a buffer in memory
- C programs begin life with three open streams (defined in $\text{stdio.h}$)
	- **stdin** (standard input)
	- **stdout** (standard output)
	- **stderr** (standard error)
```c
#include <stdio.h>
extern FILE *stdin; /* standard input (descriptor 0) */
extern FILE *stdout; /* standard output (descriptor 1) */
extern FILE *stderr; /* standard error (descriptor 2) */

int main(){
	fprintf(stdout, "Hello, world\n");
}
```
## Buffered I/O
- Motivation
	- Application often read/write one character at a time
		- $\text{getc, putc, ungetc}$
		- $\text{gets, fgets}$
			- Read line of text one character at a time, stopping at newline
	- Implementing as Unix I/O calls expensive
		- $\text{read}$ and $\text{write}$ require Unix kernel calls
			- \> 10000 clock cycles
	- Solution : Buffered read![](https://i.imgur.com/vvs69P6.png)
		- Use Unix $\text{read}$ to grab block of bytes 
		- User input functions take one byte at a time from buffer
			- Refill buffer when empty
- Standard I/O functions use buffered I/O![](https://i.imgur.com/44zxqGv.png)
- Buffer flushed to output fd on $\text{"\\n"}$, call to $\text{fflush}$ or $\text{exit}$ or return from $\text{main()}$![](https://i.imgur.com/AX8RxHG.png)
## Pros and Cons of Standard I/O
- Pros
	- Buffering increases efficiency by decreasing the number of read and write system calls
	- Short counts are handled automatically
- Cons
	- Provides no function for accessing file metadata
	- Standard I/O functions are not async-signal-safe, and not appropriate for signal handlers
	- Standard I/O is not appropriate for input and output on network sockets