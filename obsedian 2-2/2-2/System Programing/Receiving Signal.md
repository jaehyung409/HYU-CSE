## Receiving Signal
- A desination process receives a signal when it is forced by the kernel to return to react in some way to the delivery of the signal
- Some possible ways to react
	- <font color="#fac08f">Ignore</font> the signal (do nothing)
	- <font color="#fac08f">Terminate</font> the process (with optional core dump)
	- <font color="#fac08f">Catch</font> the signal by executing a user-level function called <font color="#fac08f">signal handler</font>
		- Akin to a hardware exception handler being called in response to an asynchronous interrupt
- Suppose kernel is returning from an exception handler and is ready to pass control to process p
	- ![](https://i.imgur.com/6YssGN8.png)
	- Kernel computes **pnb = pending & ~blocked**
		- The set of pending non-blocked signals for process p
	- If no pending signal to handle $\rightarrow\ \text{pnb == 0}$
		- Pass control to next instruction in the logical flow for p
	- Otherwise
		- Choose least nonzero bit k in pnb and force process p to receive signal k
		- The receipt of the signal triggers some action by p
		- Repeat for all nonzero k in pnb
		- Pass control to next instruction in logical flow for p