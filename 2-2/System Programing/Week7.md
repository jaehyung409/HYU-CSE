#hyu 
# Machine-Level Programming IV : Data
1. [[1. PROJECT/HYU-CSE/2-2/System Programing/Array|Arrays]]
	- One-dimensional
	- Multi-dimensional (nested)
	- Multi-level
2. Structures
	- Allocation
		- Generating Pointer to Array Element
			- Offset of each structure member determined at compile time
	- Access 
		- offset \# within structure (determined at compile time)
	- [[Alignment]]
3. Floating Point
	- Using Registers differ Integer
		- Using different Hardware
		- Complex and Slow
		- Using Integer is more economical
4. Summary
	- Arrays
		- Elements packed into contigious region of memory
		- Use index arithmetic to locate individual elements
	- Structures
		- Elements packed into single region of memory
		- Access using offsets determined by compiler
		- Possible require internal and external padding to ensure alignment
	- Combinations
		- Can nest structure and array code arbiterarily
	- Floating Point
		- Data held and operated on in XMM registers

# Program Optimization
1. Overview
	- _There's more to performance that <font color="#fac08f">asymptotic complexity</font>_
		- Constant factors matter too!
	- Must understand systems to optimize performance 
	- Optimizing Compilers ; 
		- Don't (usually) improve efficiency
		- <font color="#fac08f">Optimization Blockers</font>
2. [[Optimization#Generally Useful Optimizations|Generally Useful Optimizations]]
3. [[Optimization#Optimization Blockers|Optimization Blockers]]
4. Exploiting <font color="#fac08f">Instruction-Level Parallelism </font>
    >Execute multiple instructions at the same time (independent data)
	- Superscalar Processors
	- Pipelining
		- \# of stage ∝ performance
		- <font color="#fac08f">Independency</font>
	- Haswell CPU (pipelining stage)
		- 2 load
		- 1 store
		- 4 integer
		- 2 FP multiply
		- 1 FP add/divide
	- Programing with AVX2
		- ymm registers (total 16 registers, 32bytes each)
			- SIMD operations
	- Benchmark (check performance)