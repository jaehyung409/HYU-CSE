# Alignment Principles
- ### Aligned Data
	- Primitive data type requires K bytes
	- Address must be multiple of K
	- Required on some machines; advised on x86-64

| Data Type                  | Bytes | Address                               |
| -------------------------- | ----- | ------------------------------------- |
| char, ...                  | 1     | no restrictions                       |
| short, ...                 | 2     | lowest 1 bit of address must be $0_2$ |
| int, float, ...            | 4     | lowest 2 bit of address must be $00_2$ |
| double, long, char \*, ... | 8     | lowest 3 bit of address must be $000_2$ |
| long double (GCC on Linux) | 16    | lowest 4 bit of address must be $0000_2$ | 
- ### Motivation for Aligning Data
	- Memory accessed by (aligned) chunks of 4 or 8 bytes (system dependent)
		- Inefficient to load or store datum that spans quad word boundaries
		- Virtual memory trickier when datum spans 2 pages
- ### Compiler
	- Insert gaps(padding) in structure to ensure correct alignment of fields

# Alignment with Structures 
- Within structure :
	- Must satisfy each  element's alignment requirement
- Overall structure placement
	- Each structure has alignment requirement K
		- K = largest alignment of any element (primitive type)
	- Initial address & structure length must be multiples of K
- Saving Space (duty of developer)
	- Put large data types first (or reverse)