
### Symbol Resolution
- Symbol(globla variables and functions) defintions are stored in object file in ***symbol table***
	- Symbol table is an array of structs
	- Each entry includes name, size, and location of symbol
    > During symbol resolution step, the linker associates each symbol reference with <font color="#fac08f">exactly one symbol definition</font>.

### Linker Symbols 
- Global symbols
	- Symbols defined by module *m* that can be referenced by other modules
	- E.g., non-**static** C functions and nod-**static** global variables
- External symbols
	- Global symbols that are referenced by module *m* but defined by some other module
- Local symbols
	- Symbols that are defined and referenced exclusively by module *m*
	- E.g., C functions and global variables defined with the **static** attribute
		- stored in $\text{.bss}$ or $\text{.data}$
			- (cf. non-static: stored on the stack)
	- <font color="#fac08f">Local linker symbols are not local program variables!!</font>
- Duplicate Symvol Definitions
	- Strong : Procedures and initialized globals -> $\text{.data}$ section
	- Weak : Uninitialized globals -> $\text{.bss}$ section
	- ![](https://i.imgur.com/zRdAyiu.png)
- Rules
	1. Multiple strong symbols are not allowed
	2. Given a strong symbol and multiple weak symbols, choose the strong symbol
	3. If there are multiple weak symbols, pick an arbitrary one
		- Can override this with **gcc - fno-common**

### Linker Puzzles
![](https://i.imgur.com/gAEhAd8.png)
- x in p2, used in double(8 bytes), but real size of x is 4 bytes, 
	- if x = -0.0 in p2, x= 0x0, y = 0x80000000 (overwrited)

### Global Variables
- Avoid if you can
- Otherwise 
	- Use `static` if you can
	- Initialize if you define a global variable
	- Use `extern` if you reference an external global variable