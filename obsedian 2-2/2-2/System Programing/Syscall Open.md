#syscall #c #linux
## $\text{open (filename, options)}$
- User calls : $\text{open (filename, options)}$
- calls $\text{\_\_open()}$, which invokes system call $\text{syscall}$
```assembly
<__open>
...
mov $0x2, %eax # open is syscall #2
syscall        # return value in %rax
cmp $0xfffffffffffff001, %rax
...
retq
```
- $\text{\%rax}$ contains syscall number
- Return value in $\text{\%rax}$
	- Negative value is an error corresponding to negative $\text{errno}$
- ![](https://i.imgur.com/ejzxZWT.png)