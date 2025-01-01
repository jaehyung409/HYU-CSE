#bit 
## Operation : 
- ### [[Boolean Algebra]]
	 ![[Boolean Algebra#Contrast Logical Operaions|Contrast: Logical Operations]]
	- view arguments as bit vectors
	- ex) Set Representing & Manipulating Sets
		| 0 1 1 0 1 0 0 1 |  { 0, 3, 5, 6}
		| 7 <font color="#ff0000">6</font> <font color="#ff0000">5</font> 4 <font color="#ff0000">3</font> 2 1 <font color="#ff0000">0</font> |
		Intersection (&), Union(|), Symmetric defference (^), Complement (~)
	
- ### Shift Operations![[Shift Operations]]
- ### Encoding Integers
	- Unsigned ($0\  to \  2^w - 1$)
	- [[two's complement]] ($-2^{w-1} \ to \ 2^{w-1} - 1$)
	- Observations
		- $U_{min} = 0$
		- $| T_{min} | = T_{max} + 1$
			- Asymmetric range
		- $U_{max} = 2 * T_{max} + 1$
		- $-T_{min} = T_{min}\ ,\ -0 = 0$ ~ two's complement
		- C Programming with 
```c
#include <limits.h>
ULONG_MAX
LONG_MAX
LONG_MIN
```
- ### Mapping Signed <-> Unsigned
	- Conversion 
		- Signed <-> bits <-> Unsigned
- ### [[Signed vs Unsigned]]
