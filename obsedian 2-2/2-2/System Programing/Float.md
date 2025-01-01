## Fractional Binary Numbers
#### Representation
1. Bits of right of "Binary point" represent fractional powers of 2

ex)

| Decimal | Binary |
| ------- | ------ |
| 5 3/4   | 101.11 |
| 2 7/8   | 10.111 |
| 1/ 7/16 | 1.0111 |
Divide by 2 by shifting right
2. Numbers of form $0.111111..._2$ are just below 1.0 ($1.0-\epsilon$)
3. Limitation
	1. Can only exactly represent numbers of the form $x/2^k$
		- other rational numbers have repeating bit representations
	2. Just one setting of binary point within the w bits
		- Limited range of numbers (very small values? very large?)

#### IEEE floating point  standard
1. uniform standard (established in 1985)
2. Nice standards for rounding, overflow, underflow

- Numerical Form $$(-1)^s M 2^E$$
	- Sign bit $s$ determines whether numbers is negative or positive
	- Sinificand $M$ normally a fractional value in range \[1.0,2.0]
	- Exponent E weights value by power of two
	- <font color="#ddd9c3">Encoing > [S, Exponent(not equal to E), Fractional value(not equal to M)]</font>
- Single Precision ($\approx7\ decimal,\ 10^{\pm38}$, 1/8/23) Double($\approx 16\ decimal,\ 10^{\pm308}$, 1/11/52) ... half, quad

- Three kinds of floating point numbers
	- In exponent bits
	
	1. $exp\neq 0 \quad and \quad exp \neq 11...11$ (normalized)
		- Exponent coded as a a biased value : E = exp - Bias
			- exp : unsigned value of exp field
			- Bias = $2^k -1$, where k is numver of exponent bits
				- Single precision : 127 ( (256-2)/2 : denormalized, special case)
				- Double precision : 1023
		- Significand coded with implied leading 1 : M = 1.xxx...x$_2$
		- Ex) F = 15213.0 
		- $$\begin{align} &Value\\15213_{10} & = 11101101101101_2 \\&= 1.1101101101101_2 \\\\&Sinificand\\M& = 1.1101101101101_2\\frac&=\ \ .11011011011010000000000_2\\\\&Exponent&\\E&=13\\Bias&=127\\exp &= 140 = 10001100_2\end{align}$$
		- Result : 0 1001100 11011011011010000000000

	2. $exp = 00...00$ (denormalized)
		- Exponent value : E = 1  - Bias (-126, -1022 ...)
		- Significand coded with implied leading 0 : M = 0.xxx...x$_2$
		- Cases
			1. exp = 000...0, frac = 000...0
				- Represents zero value
				- Note distinct vlaues : +0 and -0(1000...00)
			2. exp = 000...0, frac $\neq$ 000...0
				- Numbers closest to 0.0
				- Equispaced


	1. $exp=11...11$ (special)
		- Cases
			1. exp = 111...1, frac = 000...0
				- Represents value $\infty$ (infinity)
			2. exp = 111...1, frac $\neq$ 000...0
				- Not-a-Number (NaN)

#### C float Decoding Example
1. float : 0xC0A00000
- binary : <font color="#b7dde8">1</font><font color="#d99694">100 0000 1</font><font color="#8db3e2">010 0000 0000 0000 0000 0000</font>
- E = exp - Bias = 129 - 127 = 2 (decimal)
- S = 1 -> negative number
- M = 1.010 0000 0000 0000 0000 0000
- M = 1.25
- v = $(-1)^sM2^E=(-1)^1 * 1.25 * 2^2 = -5$

2. float : 0x001C0000
- binary : <font color="#b7dde8">0</font><font color="#d99694">000 0000 0</font><font color="#8db3e2">001 1100 0000 0000 0000 0000</font>
- E = 1 - Bias = -126
- S = 0 -> positive number
- M = 0.001 1100 0000 0000 0000 0000
- M = 7/32
- v = $(-1)^sM2^E=(-1)^0*7*2^{-5}*2^{-126}=7*2^{-131}$
- v $\approx$ 2.571393892 X $10^{-39}$

#### Special Properites of the IEEE Encoding
- FP Zero same as Integer Zero (All bits 0)
- Can (Almost) Use Unsigned Integer Comparison
	- Must first compare sign bits
	- Must consider -0 = 0
	- NaNs problematic
	- Otherwise OK
		- Denorm vs. normalized
		- Normalized vs. infinity


#### Operations
- Basic Idea : Round.
	- First compute exact result
	- Make it fit into desired precision
- Rounding
	- Towards zero
	- Round down
	- Round up
	- Nearest Even (default) : Round to nearest, but if half-way in-between then round to nearest even
- Rounding (Nearest Even)
	- 1.BBG<font color="#e5b9b7">R</font>XXX
	- Guard bit : LSB of result
	- Round bit : 1$_{st}$ bit removed
	- Sticky bit : OR of remaining bits
	- Round up conditions 
		- Round = 1, sticky = 1 : > 0.5
		- Guard = 1, Round = 1, Sticky = 0 : Round to even

| Fraction    | G<font color="#e5b9b7">R</font>S(vs half) | Incr | Round to even |
| ----------- | ----------------------------------------- | ---- | ------------- |
| 1.000 0 000 | 0<font color="#e5b9b7">0</font>0 (<)      | N    | 1.000         |
| 1.101 0 000 | 1<font color="#e5b9b7">0</font>0 (<)      | N    | 1.101         |
| 1.000 1 000 | 0<font color="#e5b9b7">1</font>0 (=)      | N    | 1.000         |
| 1.001 1 000 | 1<font color="#e5b9b7">1</font>0 (=)      | Y    | 1.010         |
| 1.000 1 010 | 0<font color="#e5b9b7">1</font>1 (>)      | Y    | 1.001         |
| 1.111 1 100 | 1<font color="#e5b9b7">1</font>1 (>)                                   | Y    | 10.000        |
- Multiplication
	- $$(-1)^{s_1}M_12^{E_1} \times (-1)^{s_2}M_22^{E_2}$$
	- Exact Result : $(-1)^sM2^E$
		- Sign s :               $s_1 \wedge s_2$
		- Significand M :  $M_1 \times M_2$
		- Exponent E :     $E_1 + E_2$
	- Fixing
		- If M $\geq$ 2, shift M right, increment E
		- If E out of range, overflow
		- Round M to fit frac precision
	- Ex) 4 bit significand$$\begin{align}1.010*2^2 \times 1.110*2^3 &= 10.0011*2^5
	\\&=1.00011*2^6
	\\&=1.001*2^6\end{align}$$
- Addition
	- $$(-1)^{s_1}M_12^{E_1} + (-1)^{s_2}M_22^{E_2}$$
	- Assume $E_1 > E_2$
	- Exact Result : $(-1)^sM2^E$
		- Sign s, signficand M :
			- Result of signed align & add
		- Exponent E : $E_1$
	- Fixing
		- If M $\geq$ 2, shift M right, increment E
		- If M < 1, shift M left k positions, decrement E by k
		- Overflow if E out of range
		- Round M to fit frac precision
	- Ex)$$\begin{align}1.010*2^2+1.110*2^3 &=(0.1010 + 1.1100)*2^3
	\\&=10.0110*2^3
	\\&=1.00110*2^4
	\\&=1.010*2^4\end{align}$$
