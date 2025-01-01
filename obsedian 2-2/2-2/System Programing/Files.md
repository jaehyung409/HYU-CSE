## Opening Files
- Opening a file informs the kernel that you are getting ready to access that file
```c
int fd;    /* file descriptor */

if ((fd == open("/etc/hosts", O_RDONLY)) < 0) {
	perror("open");
	exit(1);
}
```
- Returns a small identifying integer *<font color="#d99694">file descriptor</font>*
	- `fd == -1` indicates that an error occured
- Each process created by a Linux shell begins life with **three open files** associated with a terminal
	- 0 : standard input (stdin)
	- 1 : standard output (stdout)
	- 2 : standard error (stderr)
## Closing Files
- Closing a file informs the kernel that you are finished accessing that file
```c
inf fd;      /* file descriptor */
int retval;  /* return value */

if ((retval = close(fd)) < 0) {
	perror("close");
	exit(1);
}
```
- Closing an already closed file is a recipe for disaster in ***threaded*** programs
- Moral : Always check return codes, even for seemingly benign functions such as $\text{close}$
## Reading Files
- Reading a file copies bytes from the current file position to memory, and then updates file position
	- Files is viewed as a sequence of bytes -> <font color="#d99694">stream</font>
```c
char buf[512];
inf fd;        /* file descriptor */
int nbytes;    /* number of bytes read */

/* Open file fd ... */
/* Then read up to 512 bytes from file fd */
if ((nbytes = read(fd, buf, sizeof(buf))) < 0) {
	perror("read");
	exit(1);
}
```
- $\text{read()}$ returns number of bytes read from file **fd** into **usrbuf** 
	- `ssize_t read(int fd, void *usrbuf, size_t n);`
- `ssize_t` vs. `size_t`
	- Calling $\text{read}$ with n bytes whose type is `size_t`
	- $\text{read}$ returns up to n bytes whose type is `ssize_t`
- `ssize_t` is <font color="#d99694">signed</font> integer (signed size_t)
	- `nbytes == sizeof(buf)`
	- `nbytes < 0` indicates that an error occured
	- `nbytes < sizeof(buf)` -> [[Short Counts]]<font color="#d99694"> (Not an error!)</font>
## Writing Files
- Writing a file copies bytes from memory to the current file position, and then updates current file position
```c
char buf[512];
inf fd;        /* file descriptor */
int nbytes;    /* number of bytes read */

/* Open file fd ... */
/* Then write up to 512 bytes from buf to file fd */
if ((nbytes = write(fd, buf, sizeof(buf))) < 0) {
	perror("write");
	exit(1);
}
```
- Returns number of bytes written from **buf** to file **fd**
	- `nbytes < 0` indicates that an error occured
	- As with reads, ***[[Short Counts]]*** are possible and are not errors!