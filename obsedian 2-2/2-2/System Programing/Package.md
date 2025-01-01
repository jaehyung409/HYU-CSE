### Packaging Commonly Used Functions
- Math, I/O, memory management, string manipulation
- Awkward, given the linker framework so far
	- <font color="#e5b9b7">Option 1</font> : Put all functions into a single source file
		- Programmers link big object file into their programs
		- Space and time inefficient
	- <font color="#e5b9b7">Option 2</font> : Put each function in a separate source file
		- Programmers explicity link appropriate binaries into their programs
		- More efficient, but burdensome on the programmer
### Old-fashioned Solution :![[Static Libraries]]
### Modern Solution : ![[Shared Libraries]]
