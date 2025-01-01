## The RIO Package
- **RIO** is a set of wrappers that provide efficient and robust I/O in apps, such as network programs that are subject to ***[[Short Counts]]***
- **RIO** provides two different kinds of functions
	- ***Unbuffered input and output*** of binary data
		- $\text{rio\_readn}$ and $\text{rio\_writen}$
	- ***Buffered input*** of text lines and binary data
		- $\text{rio\_readn}$<font color="#fac08f">b</font> and $\text{rio\_writen}$<font color="#fac08f">b</font>
		- Buffered RIO routines are thread-safe and can be interleaved arbitrarily on the same descriptor
### Unbuffered RIO Input and Output
- Same interface as Unix $\text{read()}$ and $\text{write()}$
- Especially useful for transferring data on network sockets
```c
#include "csapp.h"
ssize_t rio_readn(int fd, void *usrbuf, size_t n);
ssize_t rio_writen(int fd, void *usrbuf, size_t n);
Return : num, bytes transferred if OK, 0 on EOF (rio_readn only), -1 on error
```
- [[CSapp_h#$ text{rio _readn}$|rid_readn]] returns a [[Short Counts]] only if it encounters EOF 
	- Only use it when you know how many bytes to read
- $\text{rio\_writen}$ never returns a [[Short Counts]]
- Calls to $\text{rio\_readn}$ and $\text{rio\_writen}$ can be interleaved arbitarily on the same descriptor
### Buffered RIO Input Functions
- Efficiently read text lines and binary data from a file ***partially cached*** in an internal memory buffer
```c
#include "csapp.h"
void rio_readinitb(rio_t *rp, int fd);

ssize_t rio_readlineb(int fd, void *usrbuf, size_t maxlen);
ssize_t rio_readnb(int fd, void *usrbuf, size_t n);
Return : num, bytes read if OK, 0 on EOF, -1 on error
```
- $\text{rio\_readlineb}$ reads a text line of up to **maxlen** bytes from file **fd** and stores the line in **usrbuf**
	- Especially useful for reading text lines from network sockets
	- Stooping conditions
		- **maxlen** bytes read
		- EOF encountered
		- <font color="#fac08f">Newline ('\n') encountered</font>
- $\text{rio\_readnb}$ reads to **n** bytes from file **fd**
	- Stooping conditions
		- **maxlen** bytes read
		- EOF encountered
- Calls to $\text{rio\_readlineb}$ and $\text{rio\_readnb}$ can be interleaved arbitrarily on the same descriptor
	- Warning : Do not interleave with calls to $\text{rio\_readn}$
- #### Implementation
	- For reading from file
	- File has associated buffer to hold bytes that have been read from file but not yet read by user code![](https://i.imgur.com/8k67mdk.png)
	- ![](https://i.imgur.com/nVye1H8.png)
	- All information contained in $\text{rio\_t}$![](https://i.imgur.com/NuoD2KJ.png)
#### RIO Example
- Copying the lines of a text file from standard input to standard output
```c
#include "csapp.h"

int main(int argc, char **argv){
	int n;
	rio_t rio;
	char buf[MAXLINE];

	Rio_readinitb(&rio, STDIN_FILENO);
	while ((n = Rio_readlineb(&rio, buf, MAXLINE)) != 0)
		Rio_writen(STDOUT_FILENO, buf, n);
	exit(0);
}
```