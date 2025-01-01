### Default Actions
- Each signal type has a predefined ***default action***
	- The process **terminates**
	- The process **stops** until restarted by a $\text{SIGCONT}$ signal
	- The process **ignores** the signal
### Signal Handlers
- The $\text{signal}$ function modifies the default action associated with the receipt of signal $\text{signum}$
	- $\text{handler\_t *signal(int signum, handler\_t *handler)}$
- Different values for handler
	- $\text{SIG\_IGN}$ : ignore signals of type **signum**
	- $\text{SIG\_DFL}$ : revert to the default action on receipt of signals of type **signum**
	- Otherwise, **handler** is the address of a user-level <font color="#fac08f">signal handler</font>
		- Called when process receives signal of type **signum**
		- Referred to as "**installing**" the handler
		- Executing handler is called "**catching**" or "**handling**" the signal
		- When the handler executes its return statement, control passes back to instruction in the control flow of the process that was interrupted by receipt of the signal
```c
#include <signal.h>
/* Signal handler example */
void sigint_handler(int sig){ /* SIGINT handler */
	printf("SIGINT handler");
	exit(0);
}

int main(){
	/* Install the SIGINT handler*/
	if (signal(SIGINT, sigint_handler) == SIG_ERR)
		unix_error("signal error");
	/* Wait for the receipt of a signal */
	while(1);
	return 0;
}
```
#### Signal Handlers as Concurrent Flows
- A signal handler is a seperate logical flow (not process) that runs concurrently with the main program
	- A logical flow from $\text{main()}$
	- Another logical flow from $\text{handler()}$
	- Two logical flows belong to the same process![](https://i.imgur.com/L43g45K.png)![](https://i.imgur.com/nwTDsj7.png)
#### Nested Signal Handlers
![](https://i.imgur.com/Tp8AE5f.png)
- Handlers can be interrupted by other handlers
	- N concurrent flows in the same process
	- Concurrent flows can produce unexpected results![](https://i.imgur.com/lJ8Et1S.png)

### [[Safe Signal Handling]]
