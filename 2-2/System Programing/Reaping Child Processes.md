## Reaping Child Processes
- Idea
	- When process terminates, it still consumes system resources
		- Examples : Exit status, various OS tables
	- Called a "zombie"
		- Living corpse, half alive and half dear
- Reaping
	- Performed by parent on terminated child (using [[Syscall Wait|wait or waitpid]] )
	- Parent is given exit status information
	- Kernal then deletes zombie child process
- What if parent doesn't reap?
	- If any parent terminates without reaping a child, then orphaned child will be reaped by **init** process (pid == 1)
	- So, only need explicit reaping in long-running processes
		- e.g., shells and servers
## [[Syscall Wait|wait]] : Synchronizing with Children
- Parent reaps a child by calling the $\text{wait}$ function
- ![](https://i.imgur.com/mDxpUBm.png)
### Examples
- Zombie![](https://i.imgur.com/RS6Kx1R.png)
- Non-terminating![](https://i.imgur.com/YmRFrdo.png)
