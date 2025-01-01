#hyu #bit #byte #integer
# Bits, Bytes, and Integers
1. [[Bits]] (0 or 1)  : Electronic Implementation, Base 2
	-  Base representation in C : 0b (binary), 0x (hexadecimal)
2. Byte = 8 bits
	- Data Representation (char, short ... / Integer, real number, pointer ... )
3. [[Integer]]
     - sign extansion(<->zero extansion)
     - sign truncate
4. Representations in memory, pointers, strings
     - address is like an index ; bytes(idx)
         - idx : 4, 8, 12 (32-bit) ...or 8, 16, 24 (64-bit)  ...
5. [[Byte Ordering]]
6. Representing Strings (in C)
	- Represented by array of characters
	- string should be null-terminated
	- UTF-8 (Byte ordering not an issue !)
7. Integer C Puzzles (minly $T_min$, overflow, conversion)
	1. x < 0 -> ((x\*2) < 0)
	2. ux >= 0
	3. x & 7 == 7 -> (x<<30) < 0
	4. ux > -1
	5. x > y -> -x<-y
	6. x \* x >= 0
	7. x >0 && y >0 -> x + y > 0
	8. x >= 0  -> -x <= 0
	9. x <= 0 -> -x >= 0
	10. (x | -x) >> 31 == -1
	11. ux >> 3 == ux/8
	12. x >> 3 == x/8
	13. x & (x-1) != 0

	- Answer
		1. Tmin 
		2. <font color="#fac08f">True</font>
		3. <font color="#fac08f">True</font>
		4. conversion -1 = Umax
		5. Tmin
		6. overflow
		7. overflow
		8. <font color="#fac08f">True</font>
		9. Tmin
		10. Tmin
		11. <font color="#fac08f">True</font>
		12. when x<0...
		13. Tmin