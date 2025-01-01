![](https://i.imgur.com/hN4Avfq.png)
### Shell Programs
 - A *shell* is an application program that runs programs on behalf of the user
	- sh : Original Unix shell
	- csh/tcsh : BSD Unix C shell
	- bash : "Bourne-Again" Shell (default Linux shell)
```c
int main() {
	char cmdline[MAXLINE] /* command line */
	while(1) {
		/* read */
		printf(">");
		Fgets (cmdline, MAXLINE, stdin);
		if (feof(stdin))
			exit(0);
		/* evaluate */
		eval(cmdline)
	}
}
```
- Execution is a sequence of read/evaluate steps

#### Simple Shell $\text{eval}()$ Function
- $\text{fork()}$ -> $\text{exec()}$ : After program end, return to shell
- optional wait (foreground : wait, background : non-wait)
```c
void eval(char *cmdline) {
	char *argv[MAXARGS]; /* Argument list execve() */
	char buf[MAXLINE];   /* Holds modified command line */
	int bg;              /* Should the job run in bg or fg? */
	pid_t pid;           /* Process id */
	strcpy(buf, cmdline);
	bg = parseline(buf, argv);
	if (argv[0] == NULL)
		return;  /* Ignore empty lines */
	if (!bulitin_command(argv)) {
		if ((pid = Fork()) == 0) {  /* Chuld runs user job */
			if (execve(argv[0], argv, environ) < 0) {
				printf("%s: Command not found.\n", argv[0]);
				exit(0);
			}
		}
		/* Parent waits for foreground job to terminate */
		if (!bg) {
			int status;
			if (waitpid(pid, &status, 0) < 0)
				 unix_error("waitfg: waitpid error");
		}
		else
			prinf("%d %s", pid, cmdline);
	}
	return;
}
```
- Our example shell correctly waits for and reaps foreground jobs
- But what about background jobs?
	- Will become zombies when they terminate
	- Will never be reaped because shell (typically) will not terminate
	- Will create a memory leak that could run the kernel out of memory
- Solution : [[Exceptional Control Flow]]
	- The kernal will interrupt regular processing to alert us when a background process complets
	- In Unix, the alert mechanism is called a [[Signal]]
