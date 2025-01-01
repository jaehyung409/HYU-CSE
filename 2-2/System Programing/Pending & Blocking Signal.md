## Pending & Blocking Signal
- A signal is pending if sent but not yet received
	- There can be at most one pending signal of any particular type
	- important : Signals are <font color="#fac08f">not queued</font>
		- If a process has a pending signal of type k, then subsequent signals of type k that are sent to that process are discarded
- A process can block the receipt of certain signals
	- Blocked signals can be delivered, but will not be received untill the signal is unblocked
- A pending signal is received <font color="#fac08f">at most once</font>
	- Kernel maintains **pending** and **blocked** <font color="#fac08f">bit vectors</font> in the context of each process
		- **pending** : represents the set of pending signals
			- Kernel sets bit k in **pending** when a signal of type k is delivered
			- Kernel clears bit k in **pending** when a signal of type k is received
		- **blocked** : represents the set of blocked signals
			- Can be set and cleared by using **sigprocmask()**
			- Also referred to as the signal mask
## Blocking and Unblocking Signals
- Implicit blocking mechanism
	- Kernel blocks any pending signals of type currently being handled
	- E.g., A **SIGINT** handler can't be interrupted by another **SIGINT**
- Explicit blocking and unblocking mechanism
	- $\text{Sigprocmask()}$
- Supporting functions
	- $\text{Sigemptyset()}$ : Create empty set
	- $\text{Sigfillset()}$ : Add every signal number to set
	- $\text{Sigaddset()}$ : Add signal number to set
	- $\text{Sigdelset()}$ : Delete signal number from set
```c
#include <signal.h>
/* Blocking Signals example */
sigset_t mask, prev_mask;
Sigemptyset(&mask);
Sigaddset(&mask, SIGINT);

/* Block SIGINT and save previous blocked set */
Sigprocmask(SIG_BLOCK, &mask, &prev_mask);

/* Restore previous blocked set, unblocking SIGINT */ 
Sigprocmask(SIG_SETMASK, &prev_mask, NULL);
```