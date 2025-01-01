### Safe Signal Handling
- Some Issue : Handlers are tricky because they are concurrent with main program and share the same global data structures![](https://i.imgur.com/KutRzPM.png)
- Guidelines for Writing Safe Handlers
	- G0 : Keep your handlers as simple as possible
	- G1 : Call only async-signal-safe functions in your handlers
	- G2 : Save and restore $\text{errno}$ on entry and exit
	- G3 : Protect accesses to shared data structured by temporarily blocking all signals
	- ...
#### Async-Signal-Safety
- Function is async-signal-safe if either reentran or **non-interruptible** by signals
	- reentrant $\rightarrow$ relying on local variables (in a different stack)
	- non-interruptible $\rightarrow$ blocking signals
- Posix guarantees 117 functions to be async-signal-safe 
	- ref : "man 7 signal"
	- popular functions on the list 
		- $\text{\_exit, write, wait, waitpid, sleep, kill}$
	- Popular functions that are not on the list
		- $\text{printf, sprintf, malloc, exit}$
		- Unfortunate fact : write is the only async-signal-safe output function
### Examples
#### Correct Signal Handling
- example : ![](https://i.imgur.com/QQLLcFa.png)
- why ? 
	- ![|300](https://i.imgur.com/6bG2SuA.png)
- Must wait for all terminated child processes
	- Put $\text{wait()}$ in a loop to reap all terminated children
	- ![](https://i.imgur.com/m8lpWls.png)
#### Synchronizing Flows to Avoid Races
- SIGCHLD handler for a simple shell
	- ![](https://i.imgur.com/rX1NE44.png)
- Simple shell with a subtle synchronization error because it assumes parent runs before child
	- ![](https://i.imgur.com/6P6mE5s.png)
	- Issue
		- ![](https://i.imgur.com/YKDuBxe.png)
	- Sol
		- ![](https://i.imgur.com/X9jHxDt.png)
#### Explicitly Waiting for Signals
- Handlers explicitly waiting for SIGCHLD to arrive
	- ![](https://i.imgur.com/Y0wPGyn.png)
	- ![](https://i.imgur.com/734AoET.png)
- Program is correct, but very wasteful
- Other options : ![](https://i.imgur.com/kqJnPfe.png)
- Solution : $\text{int sigsuspend(const sigset\_t *mask)}$
	- Equivalent to atomic (or uninterruptable) version of 
		- ![](https://i.imgur.com/VNxsQYd.png)
	- ![](https://i.imgur.com/HlZPUON.png)

