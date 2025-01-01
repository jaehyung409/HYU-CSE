## How the Unix Kernel Represents Open Files
- Two descriptors referencing two distinct open files![](https://i.imgur.com/14rvGIw.png)
- Two distinct descriptors sharing the same disk file through two distinct open file table entries![](https://i.imgur.com/GMIOcf6.png)
## How Processes Share Files : $\text{fork}$
- A child process inherits its parent's open files
	- Note : situation unchanged by $\text{exec}$ functions (use $\text{fcntl}$ to change)
	- ![](https://i.imgur.com/lAnlzpV.png)![](https://i.imgur.com/o1ybXV0.png)
 