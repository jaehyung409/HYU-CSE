#### Representation
- Unsigned
- Signed
#### Expanding, Truncating
- Sing Extension.
	- Given w-bit signed integer x
	- Convert it to w+k-bit signed integer with same value
	- RULE : make k copies of MSB ; X' = k copies of MSB, $X_{w-1} ...$
- Truncate
	- Given w+k-bit signed integer x
	- Convert it to w-bit signed integer -> Values may change
	- RULE : k-bit will be removed (as overflowed k-bit) X' = (w) k bits...
	- Similar to mod, small numbers yields expected behabior.(MSB changed)

#### Operation
- Addition ([[two's complement#Operation with two's complement|ignores carry output]])
	- TAdd and UAdd have identical bit-level beavior
- Multiplication
	- Standard Multiplication Function (ignores carry)
		- some of which(carry) are different signed vs. unsigned multiplication
		- lower bits are the same
	- with Shift
		- u << k gives u * $2^k$
		- Ex) u * 24 = (u << 5) - (u << 3)
- Unsigned Power-of-2 Divide with shift
	- Quotient of Unsigned by Power of 2
		- u >> k gives ⌊u / $2^k$⌋

#### When to Use Unsigned
- Using data type : size_t
- Do use when performing *modular* arithmetic
	- Multi-precision arithmetic
- Do use when using bits to represent sets
	- Logical righ shift, no sign extension