### Signals
- ![](https://i.imgur.com/FmT8FfO.png)
- A *signal* is a small message that notifies a process that an event of some type has occurred in the system
	- Akin to exceptions and interrupts
	- Sent from the kernal (sometimes at the request of another process) to a process
	- Signal type is identified by small  integer ID's (1~30)
	- Only information in a signal is its ID and the fact that it arrived.

| ID  | Name    | Default Action | Corresponding Event                      |
| --- | ------- | -------------- | ---------------------------------------- |
| 2   | SIGINT  | Terminate      | User typed ctrl-c                        |
| 9   | SIGKILL | Terminate      | Kill program (cannot override or ignore) |
| 11  | SIGSEGV | Terminate      | Sementation violation                    |
| 14  | SIGALRM | Terminate      | Timer signal                             |
| 17  | SIGCHLD | Ignore         | Child stopped or terminated                                         |
### Signal Concepts : [[Sending Signal]]
### Signal Concepts : [[Receiving Signal]]
### Signal Concepts : [[Pending & Blocking Signal]]
### [[Signal Handlers]]
