## Jumping
	jx instructions : jump to different part of code depending on condition codes

^7fd6e1

## Conditional Moves
- Instruction supports
	- if (Test) dest <- src
- Supported in post-1995 x86 processors
- Gcc tries to use them
	- But, only when known to be safe
- WHY ?
	- Branches are very disruptive to instruction flow through *pipelines*
	- Conditional moves do not require control transfer

- Bad Cases for Conditional Move
	1. Expensive Computations
		val = Test(x) ? Hard1(x) : Hard2(x) ;
		- Both values get computed
		- Only makes sense when computations are very simple
	2. Risky Computations
		val = p ? \*p : 0;
		- Both values get computed
		- May have undesirable effects
	3. Computations with side effects
		val = x > 0 ? x*=7 : x+=3;
		- Both values get computed
		- Must be side-effect free