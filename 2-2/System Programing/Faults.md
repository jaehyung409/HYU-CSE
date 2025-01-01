### Faults
- Unintentional but possibly recoverable
- Examples : page faults (recoverable), protection faults (unrecoverable), floating point exceptions
- Either re-executes faulting ("current") instruction or aborts
#### EX : Page Fault
- User writes to memory location
- That portion (page) of user's memory is currently on disk
```c
int a[1000];
main(){
	a[500] = 13;
}
```
![](https://i.imgur.com/w3owya4.png)
#### EX : Invalid Memory Reference
- Sends $\text{SIGSEGV}$ signal to user process
- User process exits with "segmentation fault"
```c
int a[1000];
main(){
	a[5000] = 13;
}
```
![](https://i.imgur.com/hNCtCe8.png)
