## Passing control
- *Use stack to support procedure call and retuen*
- ### <font color="#e5b9b7">Procedure call </font>: call label
	- Push return address on stack
	- jump to label
- Return address :
	- Address of the next instruction right after call
	- Example from disassembly
- ### <font color="#e5b9b7">Procedure return </font>: ret
	- Pop address from stack
	- jump to address

## Passing data
| Registers   | Stack | Return value |
| ----------- | ----- |:------------:|
| %rdi(Arg 1) | Arg 7 |     %rax     |
| %rsi(Arg 2) | Arg 8 |      ^       |
| %rdx(Arg 3) | ...   |      ^       |
| %rcx(Arg 4) | ...   |      ^       | 
| %r8(Arg 5)  | Arg n |      ^       |
| %r9(Arg 6)  | ...   |      ^       |
- Only allocated stack space when needed

## Managing local data
![[Stack Frame]]

### Register Saving Conventions
	The calle and callee should be separated. (They should work without knowing each other's code)
- <font color="#e5b9b7">Caller-saved</font> (callee using)
	- **Caller** saves temporary values in its frame before the call

| Register | Usage                    | Explanation                               |
| -------- | ------------------------ | ----------------------------------------- |
| %rax     | Return value             | caller-saved, can be modified by procedure |
| %rdi     | Arguemnts                | ^                                         |
| %rsi     | Arguemnts                | ^                                         |
| %rdx     | Arguemnts                | ^                                         |
| %rcx     | Arguemnts                | ^                                         | 
| %r8      | Arguemnts                | ^                                         |
| %r9      | Arguemnts                | ^                                         |
| %r10     | Caller-saved temporaries | ^                                         |
| %r11     | Caller-saved temporaries | ^                                         |

-  <font color="#e5b9b7">Callee-saved</font> (caller using)
	- **Callee** saves temporary values in its frame before using
	- **Callee** restores them before returning to caller

| Register | Usage                             | Explanation                                                                      |
| -------- | --------------------------------- | -------------------------------------------------------------------------------- |
| %rbx     | Callee-saved temporaries          | callee-saved                                                                     |
| %r12     | Callee-saved temporaries          | ^                                                                                |
| %r13     | Callee-saved temporaries          | ^                                                                                |
| %r14     | Callee-saved temporaries          | ^                                                                                |
| %r15     | Callee-saved temporaries          | ^                                                                                |
| %rbp     | Callee-saved temporaries, Special | callee-saved, may be used as frame pointer, can mix&match                        |
| %rsp     | Special                           | special form of callee-saved, restored to orignal value upon exit frrm procedure |
