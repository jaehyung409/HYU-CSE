#linux #syscall #c
## Error Handling
- On error, Linux system-level functions typically return -1 and set global variable $\text{errno}$ to indicate cause
- Hard and fast rule :
	- We must check the return status of every system-level function
	- Only exception is the handful of functions that return $\text{void}$
### Error-reporting functions
```c
void unix_error(char *msg) /* Unix-style error */
{
	fprintf(stderr, "%s: %s\n", msg, strerror(errno));
	exit(0);
}
if ((pid = fork()) < 0)
	unix_error("fork error");
```
### Error-handling Wrappers
- We simplify the code we present to you even further by using Stevens-style error-handling wrappers 
```c
pid_t Fork(void)
{
	pid_t pid;
	if ((pid = fork()) < 0)
		unix_error("Fork error");
	return pid;
}
```