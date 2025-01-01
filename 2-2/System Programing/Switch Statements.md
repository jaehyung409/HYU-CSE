## Jump Table Structure
- VS. if-elseif-else statements
	- less operation. (one vs. many)
	- more memory (If, conditions are discontinues -> leak of memory.) 
![](https://i.imgur.com/9bjnRhJ.png)


## Indirect jump 
- ex) jmp \*.L4(,%rdi,8)
	- Start of jump table : L4
	- Must scale by factor of 8 (addresses are 8 bytes)
	- Fetch target from effective Address .L4 + x \* 8 (offset)
- determine index of Jump Table