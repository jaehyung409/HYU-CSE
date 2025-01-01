## Creating and Terminating Processes
- From a programmer's perspective, we can think of a process as being in one of three status
	- Running
		- Process is either executing, or waiting to be executed and will eventually be ***scheduled*** (i.e., chosen to execute) by the kernel
	- Stopped
		- Process execution is ***suspended*** and will not be scheduled until further notice
	- Terminated
		- Process is stopped permanently
### Terminating Processes
- Process becomes terminated for one of three reasons:
	- Returning from the $\text{main}$ routine
	- Calling the [[Syscall Exit|exit]] function
	- Receiving a signal whose default action is to terminate 
- [[Reaping Child Processes]]
### Creating Processes
- Parent process creates a new running child process by calling [[Syscall Fork|fork]]
### [[Syscall Execve|execve]] : Loading and Running Programs
