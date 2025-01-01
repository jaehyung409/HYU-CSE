#hyu
# Machine Programing III : Procedures
### Mechanisms in Procedures
- Passing control
	- To beggining of procedure code
	- Back to return point
- Passing data
	- Procedure argument
	- Return value
- Memory management
	- Allocate during procedure execution
	- Deallocate upon return
- Mechanisms all implemented with machine instructions
- x86-64 implementation of a procedure uses only those mechanisms required

### Procedures
1. [[Stack Structure]]
2. [[Calling Conventions]]
3. Illustration of Recursion
	1. Recursion means the caller and the callee are the same.
	2. Using stack frame and works similiarly.
4. Summary
	- Important Points
		- Stack is the right data structure for procedure call / return
			- If P calls Q, than Q returns before P
	- Recursion (& mutual recursion) handled by normal calling conventions
		- Can safely store values in local stack frame and in callee-saved registers
		- Put function arguments at top of stack
		- Result return in **%rax**
	- Pointers are addresses of values
		- On stack or global