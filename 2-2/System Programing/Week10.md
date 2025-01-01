#hyu 
# Exceptional Control Flow : Exceptions and Processes
0. [[Control Flow]]
1. [[Exceptional Control Flow]]
2. [[Exceptions]]
3. [[Processes]]
4. [[Process Control]]
5. Summary
	- Exceptions
		- Events that require nonstandard control flow
		- Generated externally (interrupts) or internally (traps and faults)
	- Processes
		- At any given time, system has multiple active processes
		- Only one can execute at a time on a single core, though
		- Each process appears to have total control of processor + private memory space
	- Spawning processes
		- Call $\text{fork}$
		- One call, two returns
	- Process completion
		- Call $\text{exit}$
		- One call, no return
	- Reaping and waiting for processes
		- Call $\text{wait}$ or $\text{waitpid}$
	- Loading and running programs
		- Call $\text{execve}$ (or variant)
		- One call, (normally) no return