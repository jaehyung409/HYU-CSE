### Register
![](https://i.imgur.com/CgWZaYs.png)

### BASIC : Operand src, des -> des = des Operand src
- #### Two Operand Instructions :

| Operand |  Computation   |
| ------- |:--------------:|
| add     |       +        |
| sub     |       -        |
| imul    |       \*       |
| sal     |       <<       |
| sar     | >>(Arithmetic) |
| shr     |  >>(Logical)   |
| xor     |       (^)        |
| and     |       &        |
| or      |       \|       |
- #### Single Operand Instructions : Operand des

| Operand | Computation |
| ------- |:-----------:|
| inc     |     + 1     |
| dec     |     - 1     |
| neg     |      -(neg)      |
| not     |     \~(not)      |
- #### $\text{leaq}$ : Load Effective Address
    >  메모리 접근이 없음 (mov와 다름), [05. movq와 leaq의 address 계산 방식 (tistory.com)](https://20plus3.tistory.com/46) 참조
	- Computing addresses without a memory reference
	- Computing arithmetic expressions of the form x + k\*y

### Moving Data : $\text{movq src dest}$
> movq(64-bit, movl(32-bit)) src, dest (src -> dest)
- #### Operand Types
	- Immediate ; \$0x400
	- Register ; %rax
	- Memory ; (%rax)

| Source | Dest | $\text{movq}$ Src , Dest    | C Analog     |
| ------ | ---- | --------------------------- | ------------ |
| _Imm_  | Reg  | $\text{movq}$ $0x4, %rax    | temp = 0x4;  |
| ^      | Mem  | $\text{movq}$ $-147, (%rax) | \*p = -147;  |
| _Reg_  | Reg  | $\text{movq}$ %rax, %rdx    | temp2 temp1; |
| ^      | Mem  | $\text{movq}$ %rax, (%rdx)  | \*p = temp;  |
| _Mem_  | Reg  | $\text{movq}$ (%rax), %rdx  | temp = \*p   |

- #### Simple Memory Addressing
	- Normal (R) Mem\[Reg\[R]]
		- $\text{movq}$ (%rcx), %rax
	- Displacement D(R) Mem\[Reg\[R]+D]
		- $\text{movq}$ 8(%rbp), %rdx
- #### Complete Memory Addressing Modes
	> D(Rb, Ri, S) : Mem\[Reg\[Rb] + S\*Reg\[Ri] + D]
	

### Condition Cods 
- ![[Condition Codes#Single bit registers]]
- #### Explicit Setting : $\text{cmpq b a}$
    > computing **a - b** without setting destination
- #### Explicit Setting : $\text{test a b}$
    > computing **a & b** without setting destination
- #### Reading Condition Codes : $\text{setx}$![[Condition Codes#SetX Instructions]]

### Jumping : $\text{jx label}$
![[Conditional branches#^7fd6e1]]
### Stack
- #### $\text{pushq src}$
	> Decrement %rsp by 8
	> Store value(src) at stack
- #### $\text{popq dest}$
	> Increment %rsp by 8
	> Store value at dest(register)

### Procedure : $\text{call label}, \text{ret}$
> Procedure call : **call label**
	 > - Push return_address
	 > - jmp label
	 
> Procedure return : **ret**
    > - Pop address
    > - jmp address
