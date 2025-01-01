## Processes
- An instance of a ***running program***
	- One of the most profound ideas in computer science
	- Not the same as "program" or "processor"
- Process provides each program with two key abstractions
	- <font color="#e36c09">Logical control flow</font>
		- Each program seems to have exclusive use of the CPU
		- Provided by kernal mechanism called ***context switching***
	- <font color="#e36c09">Private address space</font>
		- Each program seems th have exclusive use of main memory
		- Provided by kernal mechanism called ***virtual memory***

## Multiprocessing : The Illusion
- Computer runs many processes simultaneously
	- Applications for one or more users
		- Web browsers, email clients, editiors, ...
	- Background tasks
		- Monitoring network & I/O devices
- ![](https://i.imgur.com/Eu2dwem.png)
## Multiprocessing : The (Traditional) Reality
- ![](https://i.imgur.com/RX16Of6.png)
- Single processor executes multiple processes concurrently
	- Process executions interleaved (multitasking)
	- Address spaces managed by virtual memory system 
	- Register values for non-executing processes saved in memory
- Save current registers in memory
- <font color="#fac08f">Schedule</font> next process for execution
- Load saved registers and switch address space (context switch)
## Multiprocessing : The  (Modern) Reality
- Multicore processors
	- Multiple CPUs on single chip
	- Share main memory (and some of the caches)
	- Each can execute a separate process
		- Scheduling of processors onto cores done by kernel
## Concurrent Processes
- Each process is a logical control flow
- Two processes run ***concurrently*** (are concurrent) if their flows overlap in time
	- Concurrent : A & B, A & C
- Otherwise, they are ***sequential***
	- Sequential : B & C
- ![](https://i.imgur.com/wFeAe3M.png)
- Control flows for concurrent processes are **physically** disjoint in time
## [[Context Switching]]

