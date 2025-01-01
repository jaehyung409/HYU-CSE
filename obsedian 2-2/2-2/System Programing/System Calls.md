#syscall #c #linux 
## Ref : 
- [Introduction of System Call - GeeksforGeeks](https://www.geeksforgeeks.org/introduction-of-system-call/)
## System Calls
- System call is a way for programs to interact with the oprating system
- Each x86-64 system call has a unique ID number
- Examples :

| Number | Name                       | Description            |
| ------ | -------------------------- | ---------------------- |
| 0      | read                       | Read file              |
| 1      | write                      | Write file             |
| 2      | [[Syscall Open\|open]]     | Open file              |
| 3      | close                      | Close file             |
| 4      | stat                       | Get info about file    |
| 57     | [[Syscall Fork\|fork]]     | Create process         |
| 59     | [[Syscall Execve\|execve]] | Execute a program      |
| 60     | \_exit                     | Terminate process      |
| 62     | kill                       | Send signal to process |
Additional parts of the chart
- [[Process ID|getpid, getppid]]

## [[Error Handling]]
