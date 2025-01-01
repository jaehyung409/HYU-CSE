## Sending Signal
![](https://i.imgur.com/5nSYHC7.png)
- Kernel snds (delivers) a signal to a destination process by updating some state in the context of the destination process
- Kernel sends a siganl for one of the following reasons
	- Kernel has detected a system event such as divide-by-zero(SIGFPE) or the termination of a child process (SIGCHLD)
	- Other processes has invoked the kill system call to explicity request the kernel to send a signal to the destination process
## Process Groups
- Every process belongs to exactly one process group
![](https://i.imgur.com/TeLbDli.png)
## Sending Signals from the Keyboard
- Ctrl-C/Z causes the kernel to send a **SIGINT/SIGTSTP** to every job in the foreground process group
	- **SIGINT** : default action is to terminate each process
	- **SIGTSTP** :  default action is to stop (or suspend) each process
	- STAT (process state) Legend (ref "man ps")
		- ![|400](https://i.imgur.com/LrlrHrE.png)
		- First letter
			- S : sleeping
			- T : stopped
			- R : running
		- Second letter
			- s : session leader
			- \+ : foreground proc group
## Sending Signals with $\text{/bin/kill}$
- $\text{/bin/kill}$ program sends arbitrary signal (if -9 option : SIGKILL) to a process or process group (-pid : PID group)
- ![](https://i.imgur.com/vpz1rLT.png)
## Sending Signals with $\text{kill}$ function
- e.g., $\text{kill(pid, SIGINT)}$
	- ![](https://i.imgur.com/FBHmhbZ.png)