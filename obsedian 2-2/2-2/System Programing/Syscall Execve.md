## $\text{int execve(char *filename, char *argv[], char *envp[])}$
- Loads an runs in the current process
	- Executable file **filename**
		- Can be object file or script file beginning with $\text{\#!interpreter}$
			- e.g., $\text{\#!/bin/bash}$
		- ... with argument list **argv** (Null-terminated)
			- By convention **argv\[0] == filename**
		- ... and environment variable list **envp**
			- "name=value" strings (e.g., $\text{USER=droh}$)
			- $\text{getenv, putenv, printenv}$
- Overwrites code, data, and stack
	- Retains PID, open files and signal context
- Called <font color="#fac08f">once</font> and <font color="#fac08f">never</font> returns
	- ... except if there is an error
## Structure of Stack When a Program Starts
![](https://i.imgur.com/YQXfYXT.png)
## Example
![](https://i.imgur.com/JftRdpC.png)
