#memory

ref : [스택 메모리 소개 - GeeksforGeeks](https://www.geeksforgeeks.org/introduction-to-stack-memory/)

### Stack-Based Languages
- Languages that support recursion
	- e.g., C, Pascal, Java
	- Code must be "Reentrant"
		- Multiple simultaneous instantiations of single procedure
	- Need some place to store of each instantiaion
		- Arguments
		- Local variables
		- Return pointer
	- Stack discipline
		- State for given procedure needed for limited time
			- From when called to when return
		- Callee returns before caller does
	- Stack allocated in [[Stack Frame|Frames]]
		- state for single procedure instantiation
### x86-64 Stack
- ![](https://media.geeksforgeeks.org/wp-content/uploads/memoryLayoutC.jpg)
- Grows toward lower addresses
- Register **%rsp** contains lowest stack address 
	- address of top element

- ## push
	- **pushq** src 
		- Fetch operand at src
		- Decrement **%rsp** by 8
		- Write operand at address given by **%rsp**
- ## pop
	- **popq** dest
		- Read value at address given by **%rsp**
		- Increment **%rsp** by 8
		- Store value at dest (must be register)

