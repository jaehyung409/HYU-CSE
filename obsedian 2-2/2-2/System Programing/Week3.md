#hyu #float
# Floating Point
1. Background: [[Float#Representation|Fractional binary numbers]]
2. [[Float#IEEE floating point standard|IEEE floating point standard: Definition]]
3. [[Float#Special Properites of the IEEE Encoding|Example and properites]]
	-  Tiny case(Not realworld)
		- 8-bit Floating(1/4/3)
		- 6-bit Floating(1/3/2)
4. [[Float#Operations|Rounding, addition, multiplication]]
5. Floating point in C
	-  C Guarantees Two Levels
		- float : single precision
		- double : double precision
	- Conversions / Casting
		- double / float -> int
			- Truncates fractional part
			- Like roundling toward zero
			- Not defined when out of range or NaN : Generally sets to TMin
		- int -> double
			- Exact conversion, as long as int has $\leq$ 53 bit word size
		- int -> float
			- Will round according to rounding mode
6. Floating Point Puzzles
	1. x == (int)(float) x
	2. x == (int)(double) x
	3. f == (float)(double) f
	4. d == (double)(float) d
	5. f == -(-f)
	6. 2/3 == 2/3.0
	7. d < 0.0 -> ((d\*2) < 0.0)
	8. d > f > -f > -d
	9. d \* d >= 0.0
	10. (d+f) - d == f
	- Solves
		- 2,3,5,7,8,9 : True
```c
int x = ...;
float f = ...;
double d = ...;
``` 
7. Summary
	1. IEEE Floating Point has clear mathematical properties
	2. Represents numbers of form M x 2$^E$
	3. One can reason about operations independent of implementation
		- As if computed with perfect precision and then rounded
	4. Not the same as real arithmetic (Round)
		- violates associativity/distributivity
		- Makes life difficult for compilers & serious numerical applications programmers 