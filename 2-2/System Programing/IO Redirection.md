## I/O Redirection
- Q : How does a shell implement I/O redirection? `linux> ls > foo.txt`
	- By calling the $\text{dup2(oldfd, newfd)}$
		- Copies (per-process) descriptor table entry $\text{oldfd}$ to entry $\text{newfd}$![](https://i.imgur.com/5uKV95R.png)
### Example
- Step \#1 : open file to which stdout shoud be redirected![](https://i.imgur.com/raK6oNd.png)
- Step \#2 : call $\text{dup2(4,1)}$![](https://i.imgur.com/VZP9b9d.png)
