## Single bit registers
- CF : Carry Flag (for unsigned)
- SF : Sign Flag (for signed)
- ZF : Zero Flag
- OF : Overflow Flag (for signed)
- Implicitly set by arithmetic operations
	- *not set by leaq instruction (not for arithmetic operation).*
## Explict Setting : 
1. Compare
	- **cmpq** src2, src1
	- **cmpq b, a** like computing **a - b** without setting destination.
		- CF set when carryout from MSB or *unsigned overflow*
		- ZF set when a == b or a - b == 0
		- SF set when (a - b) < 0 (as signed)
		- OF set when two's-complement overflow or *signed overflow*
2. Test
	- **testq** src2, src1
	- **testq b, a** like computing **a & b** without setting destination.
		- ZF set when a & b == 0
		- SF set when a & b < 0

## SetX Instructions

^cfb0b2

- Set single byte(low-order byte to 0,1) based on combination of condition codes. 
- Does not alter remaining 7 bytes
	- Typically use **movzbl** to finish job (mov & rest ->zero)

| SetX  | Effect           | Descriptipn              |
| ----- | ---------------- | ------------------------ |
| sete  | ZF               | Equal / Zero             |
| setne | \~ZF             | Not Equal / Not Zero     |
| sets  | SF               | Negative                 |
| setns | \~SF             | Nonnegative              |
| setg  | \~(SF^OF) & \~ZF | Greater(Signed)          |
| setge | \~(SF^OF)        | Greater or Equal(Signed) |
| setl  | SF^OF            | Less (Signed)            |
| setle | SF^OF \| ZF      | Less or Equal (Signed)   |
| seta  | \~CF & \~ZF      | Above (Unsigned)         |
| setb  | CF               | Below (Unsigned)                         |
