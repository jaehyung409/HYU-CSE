#syscall #linux #c 

## $\text{int fork(void)}$
- Returns 0 to the child process, child’s PID to parent process
- Child is ***almost*** identical to parent
	- Child get an identical (but separate) copy of the parent’s virtual address space
	- Child gets identical copies of the parent’s open file descriptors
	- Child has a different PID than the parent
- $\text{fork}$ is interesting (and often confusing) because it is called <font color="#e36c09">once</font> but returns<font color="#e36c09"> twice</font>
- Concurrent execution
	- Can't predict execution order of parent and child
- Duplicate but separate address space
- Shared open files
	- **stdout** is the same in both parent and child

## Modeling $\text{fork}$ with [[Process Graph]]
- ![](https://i.imgur.com/ZENduma.png)
- ![](https://i.imgur.com/eZjHdLb.png)
- ![](https://i.imgur.com/NLJtKHk.png)
- ![](https://i.imgur.com/Y2LbhBa.png)

