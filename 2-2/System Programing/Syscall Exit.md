#syscall #linux #c 

## $\text{void exit(int status)}$
- Terminates with an exit status of $\text{status}$
- Convention: normal return status is 0, nonzero on error
- Another way to explicitly set the exit status is to return an integer value from the main routine
- $\text{exit}$ is called <font color="#e36c09">once</font> but<font color="#e36c09"> never</font> returns.
