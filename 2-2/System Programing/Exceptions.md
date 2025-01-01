> An exception is a transfer of control to the OS kernal in response to some event (i.e., change in processor state)
> - Kernal is the memory-resident part of the OS
> - Examples of events : Divided by 0, arithmetic overflow, page fault, I/O request completes, typing Ctrl-C
![](https://i.imgur.com/wt0UhKO.png)

### Exception Table
- Exception handlers might be implemented by SW
	- ![|400](https://i.imgur.com/m6SxILu.png)
	- Each type of event has a unique exception number k
	- k = index into exception table (a.k.a. interrupt vector)
	- Handler k is called each time exception k occurs
### Asynchronous Exceptions (Interrupts)
- Caused by events external to the processor
	- Indicated by setting the processor's ***interrupt pin***
	- Handler returns to "next" instruction
- Examples
	- Timer interrupt
		- Every few ms, an external timer chip triggers an interrupt
		- Used by the kernal to take back control from user programs
	- I/O interrupt from external device
		- Hitting Ctrl-C at the keyboard
		- Arrival of a packet from a network
		- Arrival of data from a disk
### Synchronous Exceptions
- Caused by events that occur as a result of executing an instruction
- <font color="#e36c09">Traps</font>
	- Intentional -> like procedure calls
	- Examples : **[[System Calls]]**, breakpoint traps, special instructions
	- Returns control to "next" instruction
- ![[Faults#Faults]]
- <font color="#e36c09">Aborts</font>
	- Unintentional and unrecoverable
	- Examples : illegal instruction, parity error, machine check
	- Aborts current program