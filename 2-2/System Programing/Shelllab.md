#### Make Simple Shell Function
- Built-in command 
	- quit : SIGINT (ctrl-c)
	- jobs : list of jobs
	- bg \%n : job\[n] -> bg
	- fg \%n : job\[n] -> fg
	- ctrl-c/z
- execve : run program (if \& : bg)
#### `void eval(char *cmdline)`
- main function of shell
- eval cmdline with 
	- built-in : run built-in command
	- programs : fork - execve, update job
		- if fg : wait program terminated
	- else : ignore
#### `int builtin_cmd(char **argv)`
#### `void do_bgfg(char **argv)`
#### `void waitfg(pid_t pid)`
#### `void sigchld_handler(int sig)`
#### `void sigint_handler(int sig)`
#### `void sigtstp_handler(int sig)`