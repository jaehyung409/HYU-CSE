> ### Synchronizing with Children
## $\text{pid\_t wait(int* child\_status)}$
- Suspends current process until one of its children terminates
- Return value is the **pid** of the child process that terminated
- If **child_status != NULL**, then the integer it points to will be set to a value that indicates reason the child terminated and the exit status
	- Checked using macros defined in $\text{wait.h}$
		- WIFEXITED, WEXITSTATUS, WIFSIGNALED, WTERMSIG, WIFSTOPPED, WSTOPSIG, WIFCONTINUED ... 
- If multiple children completed, will take in arbitrary order
	- Can use macros WIFEXITED and WEXITSTATUS to get information about exit status
## $\text{pid\_t waitpid(pid\_t pid, int* child\_status, int options)}$
- Suspends current process until specific process terminates
- Various options. 