#hyu 
# Machine Programing I : Basics
1. [[Computer Architecture|History of Intel processors and architectures]]
	1. 2001 : Intel Attempts Radical Shift from IA32 to IA64
	2. 2003 : AMD Steps in with Evolutionary Solution (AMD64)
	3. Intel Felt Obligated to Focus of IA64
	4. 2004 : Intel Announces EM64T extension to IA32
	5. All but low-end x86 processors support x86064
2. C, assembly, machine code
	- Architecture : The parts of a processor design that one needs to understand or write assembly/machine code (Interface / Design)
	- Microarchitecture : Implementation of the architecture
	- Code Forms 
		- Machine Code : The byte-level programs that a processor executes
			- object file, executable file
		- Assembly Code : A text representation of machine code
	- Turning C into Object Code
		- Compiler
			- Assembly (명령어 - register)
		- Assembler
			- Object
		- Linker
			- later lesson
	- Disassembling Object Code
		 - **objdump -d**
3. Assembly Basics : Register, operands, move, Arithmetic & logical operations
	1. x86 84 Integer Registers (16)
		1. %r(64-bit register)sp
	2. ![[Assembly#Moving Data $ text{movq src dest}$]]
	3. Address Computation Instruction![[Assembly#BASIC Operand src, des -> des = des Operand src]]
